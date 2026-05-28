---
type: runbook
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - runbook/pointhub
  - project/pointhub
---

# PointHub Local Development Environment

## Goal

Mac/Apple Silicon 환경에서 Docker 기반 PointHub 로컬 미들웨어 스택을 구성한다.

## Preconditions

- Docker 또는 Colima를 사용할 수 있어야 한다.
- 로컬 DB, WAR, SafeDB 설정 파일은 운영 값이 아닌 로컬/개발 값을 사용한다.
- IP, SSH alias, 계정, 키, token, 암호화 샘플 값은 이 위키에 기록하지 않는다.

## Steps

1. Docker runtime을 준비한다.
2. `middleware-stack` 같은 작업 디렉터리를 만들고 `deployments`, `config`, `logs`, `postgres` 하위 구조를 만든다.
3. PostgreSQL 컨테이너를 먼저 기동하고 로컬 DB 2개를 준비한다.
4. WildFly 계열 컨테이너는 PointHub/관리 앱 WAR와 로컬 DB를 연결한다.
5. Tomcat 계열 컨테이너는 adserver, echoserver, clipcms 역할로 분리한다.
6. SafeDB 설정 경로와 project config 경로는 JVM `-D` 옵션으로 주입한다.
7. 외부 노출이 필요한 서비스만 host port를 열고, 내부 전용 서비스는 Docker network에서만 접근하게 한다.
8. 로그와 배포 산출물은 volume으로 분리한다.

## Verification

- `docker compose ps`에서 모든 필수 컨테이너가 running/healthy 상태다.
- WildFly와 Tomcat 로그에 datasource 연결 오류가 없다.
- PointHub, 관리 앱, clipcms의 health 또는 첫 화면이 열린다.
- 로컬 PostgreSQL에 `pointhub_local`, `clip_point_db_local` 용도의 DB가 분리되어 있다.

## Rollback

- 컨테이너만 중단하려면 `docker compose down`을 사용한다.
- 로컬 DB 데이터를 버려도 되면 volume 삭제 전 백업 필요 여부를 확인한다.
- 운영/TB DB와 혼동하지 않도록 로컬 DB명에는 `_local` 접미사를 유지한다.

## Related Notes

- [[PointHub]]
- [[PointHub Local DB Migration]]
- [[PointHub Runtime and Middleware]]
- [[SafeDB Agent Setup]]

