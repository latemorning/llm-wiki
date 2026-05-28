---
type: runbook
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - runbook/tomcat
  - project/pointhub
---

# Tomcat Multi Instance Shutdown

## Goal

여러 Tomcat 인스턴스를 한 서버에서 운영할 때 `stop.sh`가 잘못된 shutdown port를 사용하거나 종료 확인 없이 끝나는 문제를 방지한다.

## Preconditions

- 각 인스턴스는 서로 다른 `CATALINA_BASE`를 가진다.
- `server.xml`의 shutdown port는 JVM property로 주입한다.
- 인스턴스별 port offset 값을 `server.sh` 또는 동등한 설정 파일에서 명시한다.

## Steps

1. 각 인스턴스의 `server.sh`에 port offset 값을 명시한다.
2. `env.sh`에서 shutdown, HTTP, AJP, SSL port를 offset 기반으로 계산한다.
3. `stop.sh`에서는 `. ./env.sh` 호출 전에 기존 `JAVA_OPTS`를 초기화한다.
4. 종료 명령은 timeout과 force 옵션을 지원하는 방식으로 호출한다.
5. 종료 후 `Dserver=<instance>` 또는 동일한 식별자로 PID가 남았는지 확인한다.
6. PID가 남아 있으면 로그를 남기고 승인된 강제 종료 절차를 수행한다.

## Verification

- 각 인스턴스의 shutdown port가 서로 다르다.
- `stop.sh` 실행 시 올바른 shutdown port가 로그에 출력된다.
- 같은 shell session에서 start 후 stop을 실행해도 이전 `JAVA_OPTS`가 재사용되지 않는다.
- 종료 후 해당 인스턴스 PID가 남아 있지 않다.

## Rollback

- offset 계산을 바꾼 뒤 문제가 생기면 기존 `server.sh`, `env.sh`, `stop.sh` 백업으로 되돌린다.
- 강제 종료는 대상 인스턴스 PID를 확인한 뒤 수행한다.

## Related Notes

- [[PointHub Runtime and Middleware]]
- [[PointHub Local Development Environment]]

