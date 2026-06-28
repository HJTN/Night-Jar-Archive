# [기능명] 개발 스펙

> 이 템플릿을 복사해서 기능별 스펙 문서로 사용하세요.
> 작성 후 관련 없는 섹션은 삭제해도 됩니다.

---

## 기능 개요

| 항목 | 내용 |
|------|------|
| 기능명 | (예: 주문 취소 API) |
| 작성자 | |
| 작성일 | |
| 상태 | 초안 / 리뷰 중 / 확정 / 개발 중 / 완료 |
| 관련 티켓 | [JIRA-123](링크) |
| 예상 완료일 | |

---

## 배경 및 목표

### 배경
이 기능이 왜 필요한가? 어떤 문제를 해결하는가?

### 목표
- [ ] (예: 사용자가 배송 전 주문을 직접 취소할 수 있다)
- [ ] (예: 취소 사유를 선택하고 기록할 수 있다)

### 범위 외 (Out of Scope)
이번 개발에서 다루지 않는 것을 명시한다.
- (예: 배송 중 주문 취소는 고객센터 처리로 이번 범위 제외)

---

## DB 스키마 변경

### 신규 테이블

```sql
-- 없으면 삭제
CREATE TABLE order_cancellations (
    id          BIGINT AUTO_INCREMENT PRIMARY KEY,
    order_id    BIGINT NOT NULL COMMENT '주문 ID',
    user_id     BIGINT NOT NULL COMMENT '취소 요청 사용자',
    reason_code VARCHAR(50) NOT NULL COMMENT '취소 사유 코드',
    reason_text VARCHAR(500) COMMENT '취소 사유 상세',
    canceled_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_cancellation_order FOREIGN KEY (order_id) REFERENCES orders(id)
);
CREATE INDEX idx_order_cancellations_order_id ON order_cancellations(order_id);
```

### 기존 테이블 변경

```sql
-- 없으면 삭제
ALTER TABLE orders
    ADD COLUMN status VARCHAR(20) NOT NULL DEFAULT 'PENDING' COMMENT '주문 상태' AFTER total_amount,
    ADD COLUMN canceled_at DATETIME COMMENT '취소 시각';
```

### 마이그레이션 파일
- 파일명: `V20240115__add_order_cancellation.sql`
- 롤백 스크립트: (롤백 방법 기술 또는 별도 파일 경로)

---

## API 스펙

### 엔드포인트 목록

| 메서드 | 경로 | 설명 | 인증 필요 |
|--------|------|------|----------|
| POST | `/api/orders/{orderId}/cancel` | 주문 취소 | O |

---

### POST /api/orders/{orderId}/cancel

**요청**

```
POST /api/orders/123/cancel
Authorization: Bearer {accessToken}
Content-Type: application/json
```

```json
{
  "reasonCode": "CHANGE_MIND",
  "reasonText": "단순 변심으로 취소합니다."
}
```

**Path Parameters**

| 파라미터 | 타입 | 필수 | 설명 |
|---------|------|------|------|
| orderId | Long | O | 취소할 주문 ID |

**Request Body**

| 필드 | 타입 | 필수 | 유효성 | 설명 |
|------|------|------|--------|------|
| reasonCode | String | O | Enum 값 중 하나 | 취소 사유 코드 |
| reasonText | String | X | 최대 500자 | 취소 사유 상세 |

**취소 사유 코드 (reasonCode)**

| 코드 | 설명 |
|------|------|
| CHANGE_MIND | 단순 변심 |
| WRONG_ORDER | 주문 실수 |
| DELIVERY_DELAY | 배송 지연 |

**응답 - 성공 (200 OK)**

```json
{
  "orderId": 123,
  "status": "CANCELED",
  "canceledAt": "2024-01-15T10:30:00"
}
```

**응답 - 실패**

| HTTP 상태 | errorCode | 설명 |
|----------|-----------|------|
| 400 | INVALID_REASON_CODE | 유효하지 않은 취소 사유 코드 |
| 403 | FORBIDDEN | 다른 사용자의 주문 취소 시도 |
| 404 | ORDER_NOT_FOUND | 주문을 찾을 수 없음 |
| 409 | ALREADY_CANCELED | 이미 취소된 주문 |
| 409 | CANNOT_CANCEL_SHIPPED | 이미 배송 시작된 주문 |

```json
{
  "errorCode": "CANNOT_CANCEL_SHIPPED",
  "message": "이미 배송이 시작된 주문은 취소할 수 없습니다."
}
```

---

## 비즈니스 로직

### 취소 가능 조건
1. 요청자가 해당 주문의 소유자이어야 한다
2. 주문 상태가 `PENDING` 또는 `CONFIRMED`이어야 한다 (`SHIPPED`, `DELIVERED`, `CANCELED` 상태는 취소 불가)
3. 주문 생성 후 72시간 이내이어야 한다 (정책)

### 취소 처리 절차
1. 주문 상태를 `CANCELED`로 변경
2. 취소 이력(`order_cancellations`) 저장
3. 결제 취소 요청 (결제 서비스 API 호출)
4. 재고 복구 (재고 서비스 이벤트 발행 또는 직접 호출)
5. 취소 완료 알림 발송 (알림 서비스 이벤트 발행)

### 트랜잭션 처리
- 주문 상태 변경 + 취소 이력 저장은 동일 트랜잭션
- 결제 취소·재고 복구·알림은 별도 트랜잭션 또는 메시지 큐로 비동기 처리
- 결제 취소 실패 시 보상 트랜잭션 처리 방법: (기술)

---

## 예외 케이스

| 케이스 | 처리 방법 |
|--------|----------|
| 동시에 같은 주문 취소 요청 | DB 낙관적 락 또는 비관적 락으로 중복 처리 방지 |
| 결제 취소 API 실패 | 재시도 큐에 등록, 수동 처리 알림 발송 |
| 취소 중 서버 다운 | 주문 상태 `CANCELING`으로 중간 상태 관리, 복구 Job 운영 |
| 이미 배송 출발 후 취소 요청 | 409 CANNOT_CANCEL_SHIPPED 반환, 고객센터 안내 |

---

## 테스트 계획

### 단위 테스트 (`OrderCancelServiceTest`)
- [ ] 정상 취소 - PENDING 상태 주문
- [ ] 정상 취소 - CONFIRMED 상태 주문
- [ ] 실패 - 이미 취소된 주문 (ALREADY_CANCELED)
- [ ] 실패 - 배송 시작된 주문 (CANNOT_CANCEL_SHIPPED)
- [ ] 실패 - 다른 사용자의 주문 (FORBIDDEN)
- [ ] 실패 - 72시간 초과 주문

### 통합 테스트 (`OrderCancelControllerTest`)
- [ ] POST /api/orders/{orderId}/cancel - 성공 시나리오
- [ ] POST /api/orders/{orderId}/cancel - 인증 없이 요청 시 401

### 수동 테스트 시나리오 (QA용)
1. 정상 주문 생성 → 취소 → 취소 완료 확인
2. 배송 중 주문 취소 시도 → 에러 메시지 확인
3. 동시 취소 요청 2건 → 1건만 성공 확인

---

## 기타 고려사항

- **모니터링**: 취소율 지표 추가 (`order.cancel.count` by reasonCode)
- **알림**: 취소 완료 후 이메일/푸시 발송 필요 여부 확인 (알림팀 협의 필요)
- **관련 문서**: [[Feature-Development-Flow]], [[Code-Review-Checklist]]
