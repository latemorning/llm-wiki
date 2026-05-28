---
type: system
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - system/pointhub
  - system/middleware
  - project/pointhub
---

# PointHub Runtime and Middleware

## Purpose

PointHub 관련 WAS, Tomcat, KeyVault, SafeDB, 로깅 설정의 관리 방향을 정리한다.

## Responsibilities

- 미들웨어 기동 스크립트에서 SafeDB 설정 경로, 프로젝트 설정 경로, Spring profile을 주입한다.
- 운영, 개발, 개인 로컬 환경의 JVM 옵션은 값만 다르고 구조는 동일하게 유지한다.
- KeyVault/properties는 용도별로 분리하고 최종적으로 시스템 파라미터 관리 체계로 단순화한다.
- DB connection pool은 HikariCP, 로깅 facade는 SLF4J로 표준화하는 방향을 검토한다.
- Azure 또는 미들웨어 환경에서 불필요한 DB 조회 결과 로그가 출력되지 않도록 서버 설정을 확인한다.

## Inputs

- WAS/Tomcat `env.sh`, `server.properties`, JVM `-D` 옵션
- KeyVault 설정 디렉터리
- SafeDB 설정 디렉터리
- Spring profile
- 프로젝트별 properties

## Outputs

- 환경별 일관된 JVM 옵션
- 소스 빌드와 환경 설정의 분리
- 로그 출력 수준 통제
- properties 관리 포인트 축소

## Dependencies

- [[PointHub SafeDB Encryption]]
- [[SafeDB Agent Setup]]
- [[Tomcat Multi Instance Shutdown]]

## Failure Modes

- 운영 경로, 서버명, 계정, 키 값을 문서나 커밋에 남기면 안 된다.
- 하나의 properties 파일에 DB, API 키, 시스템 설정이 과도하게 섞이면 Azure 전환과 배포 시 설정 오류가 늘어난다.
- 프로젝트별로 DB URL 형식이나 로깅 라이브러리가 다르면 장애 분석과 운영 자동화가 어려워진다.
- `cardpointswap`처럼 다른 프로젝트에 종속적으로 import되는 모듈은 설정 로딩 시점 차이로 오류가 발생할 수 있다.

## Related Notes

- [[PointHub]]
- [[PointHub Local Development Environment]]
- [[PointHub Context Pack]]

## Needs Verification

- HikariCP/SLF4J 표준화가 실제로 결정됐는지 여부
- `cardpointswap`과 `adserver` 통합 여부
- `clipcms` 메뉴의 `phubONM` 이관 여부

