---
type: decision
status: proposed
created: 2026-05-28
updated: 2026-05-28
tags:
  - decision/pointhub
  - project/pointhub
---

# 0002 Standardize PointHub Runtime Stack

## Decision

PointHub 관련 Java 프로젝트의 connection pool, logging facade, properties 관리, 일부 모듈 경계를 표준화하는 방향을 검토한다.

## Context

- 프로젝트별 DB 접속 URL 형식과 connection pool이 달라 Azure 전환과 설정 검증 비용이 컸다.
- 로깅 라이브러리가 프로젝트별로 달라 로그 정책과 장애 분석이 일관되지 않다.
- Azure 전환 중 다수 properties를 하나로 합치면서 사용하지 않는 값과 민감 값이 섞였다.
- 일부 JAR 모듈은 독립 실행보다 다른 프로젝트에 종속적으로 import되는 용도가 강하다.
- `clipcms` 일부 메뉴는 다른 관리 프로젝트로 이관할 수 있고, 남는 서버 자원은 echo server 용도로 검토할 수 있다.

## Proposed Direction

- connection pool은 HikariCP로 통일한다.
- logging facade는 SLF4J로 통일한다.
- properties는 DB, API, 시스템 설정 등 용도별로 분리하고 최종적으로 시스템 파라미터 관리 체계로 통합한다.
- 종속적 JAR 모듈은 실제 runtime ownership 기준으로 통합 여부를 검토한다.
- 메뉴 이관 후 남는 서버 자원은 echo server와 Netty thread 설정 개선에 활용할 수 있는지 검토한다.

## Consequences

- 설정 로딩 시점 차이와 properties 혼선이 줄어든다.
- 장애 분석 시 로그 포맷과 logging API가 단순해진다.
- 초기 전환 작업에서는 프로젝트별 datasource, logging bridge, 배포 산출물 검증이 필요하다.
- 모듈 통합은 패키지 충돌, 빌드 순서, 배포 ownership 재정의가 필요하다.

## Related Notes

- [[PointHub Runtime and Middleware]]
- [[PointHub SafeDB Encryption]]
- [[PointHub]]

## Needs Verification

- 이 방향이 실제 승인된 결정인지, 아직 제안인지 확인해야 한다.
- 각 프로젝트별 현재 connection pool과 logging dependency를 코드 기준으로 확인해야 한다.

