---
type: system
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - system/pointhub
  - project/pointhub
---

# PointHub Application Structure

## Purpose

PointHub 코드베이스의 주요 소스, 리소스, 웹 애플리케이션 영역을 LLM이 빠르게 파악할 수 있게 정리한다.

## Responsibilities

- `api`: 도메인별 모듈을 둔다.
- `common`: 애플리케이션 내부 공통 코드를 둔다.
- `exam`: 로컬 개발 환경에서 사용하는 테스트성 코드를 둔다. 생산 프로파일에서는 제외된다.
- `performance`: 성능 테스트용 코드를 둔다. 생산 프로파일에서는 제외된다.
- `resources/config/spring`: Spring 설정 파일을 둔다.
- `resources/mapper`: MyBatis 매퍼 XML을 둔다.
- `resources/properties`: 애플리케이션 속성 파일을 둔다.
- `resources/wsdl`: WSDL 파일을 둔다.
- `webapp`: 웹 디스크립터, 정적 리소스, JSP, terms HTML 파일을 둔다.

## Inputs

- Spring MVC가 처리하는 웹 요청
- MyBatis 매퍼 XML과 SQL 변경
- Spring 설정, 속성 파일, WSDL 리소스
- Maven 빌드 프로파일

## Outputs

- `target` 아래에 생성되는 WAR 패키지
- JSP와 정적 리소스를 포함한 웹 애플리케이션 산출물

## Dependencies

- Java 17
- Spring MVC
- Spring Mobile
- MyBatis
- JSP
- Maven

## Failure Modes

- SQL 변경을 관련 mapper XML에 반영하지 않으면 런타임 쿼리 동작이 깨질 수 있다.
- `properties`, `WEB-INF`, mapper XML 변경은 보안 또는 배포 환경 차이를 만들 수 있다.
- 생산 프로파일 제외 설정이 깨지면 로컬/테스트용 코드나 리소스가 배포 산출물에 포함될 수 있다.

## Related Notes

- [[PointHub]]
- [[PointHub Build and Test]]
- [[PointHub Context Pack]]

## Needs Verification

- 실제 웹 요청 진입점과 컨트롤러 패키지 구조
- 배포 환경별 설정 파일 분리 방식
