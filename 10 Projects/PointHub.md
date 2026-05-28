---
type: project
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - project/pointhub
  - stack/java
  - stack/spring
---

# PointHub

## Summary

PointHub는 Java 17 기반 Spring MVC 웹 애플리케이션이며 Maven으로 빌드해 WAR 패키지로 배포한다.

## Current State

- 메인 코드는 `src/main/java/com/olleh/pointhub` 아래에 있다.
- 도메인 모듈은 `api`, 공유 코드는 `common`에 둔다.
- `exam`은 로컬 개발 환경용 테스트 코드, `performance`는 성능 테스트 코드이며 생산 프로파일에서 제외된다.
- MyBatis 매퍼 XML은 `src/main/resources/mapper` 아래에 있다.
- 웹 디스크립터, 정적 리소스, JSP, 약관 HTML은 `src/main/webapp` 아래에 있다.

## Tech Stack

- Java 17
- Spring MVC
- Maven
- MyBatis
- JSP
- WAR deployment
- Spring Mobile

## Main Directories

- `src/main/java/com/olleh/pointhub/api`: 도메인별 모듈
- `src/main/java/com/olleh/pointhub/common`: 애플리케이션 공통 코드
- `src/main/java/com/olleh/pointhub/exam`: 로컬 개발/테스트용 코드, 생산 프로파일 제외
- `src/main/java/com/olleh/pointhub/performance`: 성능 테스트 코드, 생산 프로파일 제외
- `src/main/resources/config/spring`: Spring 설정 파일
- `src/main/resources/mapper`: MyBatis 매퍼 XML
- `src/main/resources/properties`: 속성 파일
- `src/main/resources/wsdl`: WSDL 파일
- `src/main/webapp`: 웹 애플리케이션 구성 요소
- `src/test/java`, `src/test/resources`: 테스트 코드와 리소스
- `pom.xml`: Maven 빌드 정의

## Commands

```bash
mvn clean package
mvn clean package -Pprod
mvn test -Dmaven.test.skip=false
```

## Conventions

- UTF-8 인코딩과 Java 17을 기준으로 한다.
- 들여쓰기는 4칸을 사용한다.
- 패키지 이름은 소문자, 클래스 이름은 PascalCase, 메소드와 필드는 camelCase를 사용한다.
- 일반 접미사는 `Controller`, `Service`, `ServiceImpl`, `Dao`, `Vo`를 따른다.
- SQL 변경은 관련 `src/main/resources/mapper/**/sql-*.xml` 파일에 반영한다.
- 커밋 메시지 형식은 `[브랜치명] 한글 요약`을 사용한다.

## Risks

- 비밀번호, API 키, 주민등록번호, 전화번호, 파트너 자격 증명은 문서나 커밋에 남기지 않는다.
- `.gitleaks.toml`과 `.githooks` 활성화 상태를 유지한다.
- `properties`, `WEB-INF`, mapper XML은 설정과 보안 영향이 큰 영역이므로 변경 전후를 주의 깊게 검토한다.
- 생산 빌드에서는 `exam`, `performance`, local MyBatis, exam mapper 리소스가 제외되어야 한다.
- 테스트는 기본적으로 건너뛸 수 있으므로 필요할 때 명시적으로 `mvn test -Dmaven.test.skip=false`를 실행한다.

## LLM Context

- 짧은 작업 맥락이 필요하면 [[PointHub Context Pack]]을 먼저 사용한다.
- 소스 구조를 파악할 때는 [[PointHub Application Structure]]를 추가한다.
- 빌드, 테스트, PR 준비는 [[PointHub Build and Test]]를 사용한다.

## Related Notes

- [[PointHub Application Structure]]
- [[PointHub Build and Test]]
- [[PointHub Context Pack]]

## Open Questions

- 실제 소스 저장소 위치
- 로컬 실행 방법
- 배포 환경별 설정 차이
- 테스트가 실제로 통과하는 기준
