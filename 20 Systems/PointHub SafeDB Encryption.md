---
type: system
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - system/pointhub
  - system/safedb
  - project/pointhub
---

# PointHub SafeDB Encryption

## Purpose

PointHub의 개인정보 암호화 전환 작업에서 SafeDB가 맡는 역할과 코드/DB 변경 범위를 정리한다.

## Responsibilities

- 개인정보성 값은 평문 컬럼 대신 SafeDB 암호화 컬럼에 저장한다.
- 암호화 저장 컬럼은 `_enc`, 검색 보조 컬럼은 `_sch` 접미사를 사용한다.
- PG별 암호화키와 시스템 파라미터는 평문 저장을 피하고 SafeDB 또는 시스템 파라미터 관리 체계로 통합한다.
- API 로그, reward 이력, 약관/포인트 API 테스트 과정에서 CI, 전화번호, 이름, 생년월일 같은 값이 노출되지 않도록 한다.
- 상속형 테이블에서 선언형 파티션 또는 시퀀스 기반 입력으로 전환할 때 컬럼/제약조건 정합성을 확인한다.

## Inputs

- SafeDB SDK와 INISAFENet 런타임
- `INISAFENet_Server.properties`
- `SafeDBMap_config.xml`
- 정책 서버/에이전트 설정
- 암호화 대상 DDL 변경 스크립트
- Java 암복호화 유틸리티와 MyBatis 매퍼

## Outputs

- `_enc` 암호화 컬럼
- `_sch` 검색용 컬럼
- SafeDB로 암호화된 시스템 파라미터
- 마스킹된 WAS/server 로그
- 암호화 적용 후 검증 가능한 API 테스트 절차

## Dependencies

- [[SafeDB Agent Setup]]
- [[PointHub Application Structure]]
- MyBatis mapper XML
- Java 17
- PostgreSQL
- INISAFENet/SafeDB SDK

## Failure Modes

- 운영 DDL 또는 properties 원문을 문서에 복사하면 스키마, 서버, 키, 인증 정보가 유출될 수 있다.
- `_enc`, `_sch` 컬럼을 일부 테이블에만 반영하면 상속형/선언형 테이블 간 컬럼 불일치가 생길 수 있다.
- 테스트용 암복호화 endpoint 결과를 그대로 저장하면 개인명, 전화번호, CI, 암호문이 유출될 수 있다.
- API 로그 해제나 디버그 로그가 남아 있으면 암호화 전후 값이 서버 로그에 출력될 수 있다.
- `DELETE FROM user_token_info` 같은 초기화성 유틸리티는 운영 데이터 손실 위험이 있으므로 격리된 환경에서만 사용한다.

## Related Notes

- [[PointHub]]
- [[PointHub Runtime and Middleware]]
- [[PointHub Local DB Migration]]
- [[PointHub Context Pack]]

## Needs Verification

- 현재 적용된 암호화 대상 테이블과 컬럼 최종 목록
- `_enc`, `_sch` 컬럼 생성 스크립트의 최신본 위치
- SafeDB 정책 서버와 에이전트 운영 절차의 승인된 기준

