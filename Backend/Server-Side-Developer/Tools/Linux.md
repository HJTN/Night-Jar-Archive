# Linux

> 서버 운영체제 및 CLI 환경

## Overview

대부분의 서버는 Linux에서 실행된다. 서버 개발자는 배포된 서버에 SSH로 접속해 프로세스 상태 확인, 로그 분석, 네트워크 진단을 수행할 수 있어야 한다.

## 프로세스 관리

```bash
# 실행 중인 프로세스 확인
ps aux | grep java          # java 프로세스 찾기
ps aux | grep '[j]ava'      # 그 자체가 검색 결과에 포함되지 않도록

# 실시간 프로세스 모니터링
top                         # 기본 (q로 종료)
htop                        # 컬러 UI (별도 설치 필요)

# 특정 포트를 사용하는 프로세스 찾기
lsof -i :8080               # 8080 포트 사용 프로세스
ss -tulnp | grep 8080       # 더 빠른 대안

# 프로세스 종료
kill -9 <PID>               # 강제 종료 (SIGKILL)
kill -15 <PID>              # 정상 종료 요청 (SIGTERM, 권장)
pkill -f 'java.*myapp'      # 패턴으로 프로세스 종료
```

## 네트워크 진단

```bash
# 포트 및 연결 확인
netstat -tulnp              # 열린 포트 목록 (구버전)
ss -tulnp                   # 열린 포트 목록 (최신)

# HTTP 요청 테스트
curl -v http://localhost:8080/health           # 상세 요청/응답 출력
curl -X POST http://localhost:8080/api/orders \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"productId": 1, "quantity": 2}'
curl -w "\n응답시간: %{time_total}s\n" http://localhost:8080/api

# DNS 및 연결
ping google.com
nslookup db.internal.com    # DNS 조회
telnet db-host 3306         # TCP 연결 가능 여부 확인
```

## 로그 확인

```bash
# 로그 파일 실시간 추적
tail -f /var/log/app/application.log
tail -f /var/log/app/application.log | grep ERROR   # 에러만 필터

# 최근 N줄 확인
tail -n 200 application.log
head -n 50 application.log

# 로그 검색
grep "NullPointerException" application.log
grep -n "ERROR" application.log | head -20          # 줄 번호와 함께, 20개만
grep -A 5 -B 2 "OutOfMemoryError" application.log   # 전후 문맥 포함

# 로그 파일 크기 확인
ls -lh /var/log/app/
du -sh /var/log/app/                                # 디렉토리 총 크기
```

## 파일 시스템

```bash
# 디스크 사용량 확인
df -h                       # 전체 디스크 사용량
du -sh /var/log/*           # 각 디렉토리 크기

# 파일 찾기
find /var/log -name "*.log" -mtime -1   # 최근 1일 이내 수정된 .log 파일
find /app -name "*.jar" -size +100M     # 100MB 이상 jar 파일

# 파일 조작
cp -r /app/config /app/config.bak       # 백업
chmod 644 application.properties        # 파일 권한 (rw-r--r--)
chown appuser:appgroup /app/logs        # 소유권 변경
```

## 서비스 관리 (systemctl)

```bash
# 서비스 상태 및 관리
systemctl status myapp              # 서비스 상태 확인
systemctl start myapp               # 서비스 시작
systemctl stop myapp                # 서비스 중지
systemctl restart myapp             # 서비스 재시작
systemctl enable myapp              # 부팅 시 자동 시작 설정
journalctl -u myapp -f              # systemd 서비스 로그 실시간 확인
journalctl -u myapp --since "1 hour ago"  # 최근 1시간 로그
```

## 성능 분석

```bash
# CPU/메모리 사용량
vmstat 1 5                  # 1초 간격으로 5번 시스템 통계 출력
free -h                     # 메모리 사용량 (human-readable)
cat /proc/cpuinfo | grep "cpu cores"   # CPU 코어 수

# JVM 힙 덤프 (OOM 분석)
jmap -dump:format=b,file=heapdump.hprof <PID>
jstack <PID> > threaddump.txt          # 스레드 덤프 (데드락 분석)

# 열린 파일 디스크립터 수 (Too many open files 에러 분석)
lsof -p <PID> | wc -l
cat /proc/<PID>/limits | grep "open files"
```

## 유용한 조합 명령어

```bash
# 에러 빈도 집계
grep ERROR application.log | awk '{print $5}' | sort | uniq -c | sort -rn | head -10

# 특정 시간대 로그 추출
awk '/2024-01-15 10:00/,/2024-01-15 10:05/' application.log

# 응답 코드별 카운트
grep "HTTP/1.1" access.log | awk '{print $9}' | sort | uniq -c | sort -rn
```

## References

- [Linux Command Line Cheat Sheet](https://cheatography.com/davechild/cheat-sheets/linux-command-line/)
- [The Linux Command Line (무료 온라인 책)](https://linuxcommand.org/tlcl.php)
