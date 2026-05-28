---
type: context-pack
status: draft
created: 2026-05-28
updated: 2026-05-28
tags:
  - context/pointhub
  - project/pointhub
---

# PointHub Context Pack

## Use This When

PointHub 코드 수정, 리뷰, 구조 파악, 빌드/테스트 관련 질문을 LLM에게 요청할 때 사용한다.

## Project Facts

- PointHub는 Java 17 기반 Spring MVC 웹 애플리케이션이다.
- Maven으로 빌드하며 WAR 패키지로 배포한다.
- 메인 코드는 `src/main/java/com/olleh/pointhub` 아래에 있다.
- 도메인 모듈은 `api`, 공유 코드는 `common`에 있다.
- MyBatis 매퍼 XML은 `src/main/resources/mapper` 아래에 있다.
- 웹 리소스와 JSP는 `src/main/webapp` 아래에 있다.
- Spring Mobile로 모바일 디바이스 감지 기능을 사용한다.
- 생산 빌드에서는 `exam`, `performance`, local MyBatis, exam mapper 리소스를 제외한다.

## Commands

```bash
mvn clean package
mvn clean package -Pprod
mvn test -Dmaven.test.skip=false
```

## Conventions

- Java 17
- 4칸 들여쓰기
- 클래스 이름은 PascalCase
- 메소드와 필드는 camelCase
- 일반 접미사는 `Controller`, `Service`, `ServiceImpl`, `Dao`, `Vo`
- SQL 변경은 관련 MyBatis XML 파일에 반영한다.

## Cautions

- 비밀번호, API 키, 주민등록번호, 전화번호, 파트너 자격 증명은 문서나 커밋에 남기지 않는다.
- `.gitleaks.toml`과 `.githooks` 활성화 상태를 유지한다.
- `properties`, `WEB-INF`, mapper XML은 민감한 변경 가능성이 높다.
- SQL 변경은 관련 `src/main/resources/mapper/**/sql-*.xml` 파일에 반영한다.
- SafeDB 테스트값, 암호문, CI, 전화번호, 개인명, PRD DDL 원문은 위키에 저장하지 않는다.
- 운영/TB IP, SSH alias, 토큰, 키, 인증서, 개인키, 라이선스 값은 placeholder로만 적는다.

## Relevant Files

- `pom.xml`
- `src/main/java/com/olleh/pointhub`
- `src/main/resources/config/spring`
- `src/main/resources/mapper`
- `src/main/resources/properties`
- `src/main/resources/wsdl`
- `src/main/webapp`

## Supporting Notes

- [[PointHub]]
- [[PointHub Application Structure]]
- [[PointHub SafeDB Encryption]]
- [[PointHub Runtime and Middleware]]
- [[PointHub Card Cancel C160]]
- [[PointHub Build and Test]]
- [[PointHub Local Development Environment]]
- [[PointHub Local DB Migration]]
- [[SafeDB Agent Setup]]
- [[Tomcat Multi Instance Shutdown]]
- [[PointHub CI CD Deployment]]

## Needs Verification

- 실제 저장소 위치
- 로컬 실행 절차
- 운영 배포 절차
- 테스트 통과 기준
