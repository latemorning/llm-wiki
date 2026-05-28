---
type: runbook
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - runbook/pointhub
  - runbook/database
  - project/pointhub
---

# PointHub Local DB Migration

## Goal

TB 또는 개발 DB의 필요한 스키마를 로컬 PostgreSQL 컨테이너로 복제한다.

## Preconditions

- 원격 DB 접속 권한과 네트워크 접근이 있어야 한다.
- `pg_dump`, `pg_restore`, `psql` 버전은 원격 PostgreSQL 버전과 호환되어야 한다.
- 덤프 파일에는 운영 개인정보와 암호화 컬럼이 포함될 수 있으므로 git, 위키, 공유 폴더에 보관하지 않는다.
- 로컬 DB명은 운영/TB와 혼동되지 않도록 `_local` 접미사를 사용한다.

## Steps

1. 원격 DB에서 필요한 스키마만 custom format으로 dump한다.
2. 소유권/권한 이식 문제를 피하려면 `--no-owner --no-privileges` 옵션을 사용한다.
3. 대용량 암호화 테이블은 필요하면 제외하고 별도 절차로 다룬다.
4. 재복원 시에는 로컬 스키마를 백업하거나 폐기 가능 여부를 확인한 뒤 drop/create한다.
5. `pg_restore`로 로컬 DB에 복원한다.
6. 오류가 나면 verbose 로그에서 실제 실패 원인을 확인한다.
7. 원격/로컬의 테이블 수, row estimate, 주요 query를 비교한다.
8. 미들웨어 datasource가 로컬 DB를 보도록 설정하고 WAS 로그를 확인한다.

## Verification

- `pg_restore`가 치명 오류 없이 종료된다.
- 로컬 스키마에 주요 테이블과 시퀀스가 존재한다.
- row count 또는 `pg_stat_user_tables` 기준으로 원격과 큰 차이가 없다.
- WildFly/Tomcat datasource 연결 로그가 정상이다.

## Rollback

- 로컬 복원 실패 시 대상 스키마를 drop/create 후 다시 복원한다.
- 덤프 파일이 손상됐거나 restore 버전이 낮으면 dump/restore 도구 버전을 맞춘다.
- 로컬 데이터만 대상으로 처리하고 원격 DB에는 destructive SQL을 실행하지 않는다.

## Related Notes

- [[PointHub Local Development Environment]]
- [[PointHub SafeDB Encryption]]
- [[PointHub Runtime and Middleware]]

