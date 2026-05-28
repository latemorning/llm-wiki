---
type: runbook
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - runbook/pointhub
  - project/pointhub
---

# PointHub Build and Test

## Goal

PointHub를 개발용 또는 생산용 WAR로 빌드하고, 필요한 경우 JUnit 테스트를 명시적으로 실행한다.

## Preconditions

- Java 17과 Maven을 사용할 수 있어야 한다.
- `pom.xml`이 있는 PointHub 코드베이스 루트에서 실행한다.
- 비밀번호, API 키, 주민등록번호, 전화번호, 파트너 자격 증명은 명령 출력이나 커밋에 남기지 않는다.

## Steps

1. 변경 전후에 `git status`로 의도한 파일만 수정되었는지 확인한다.
2. 개발용 WAR가 필요하면 `mvn clean package`를 실행한다.
3. 생산용 WAR가 필요하면 `mvn clean package -Pprod`를 실행한다.
4. 테스트가 필요하면 `mvn test -Dmaven.test.skip=false`를 실행한다.
5. PR을 준비할 때 변경 내용, 영향받는 API/mapper, 실행한 테스트 명령어, 설정 변경, 배포 영향을 정리한다.

## Verification

- Maven 명령이 exit code 0으로 끝난다.
- WAR 빌드가 필요한 경우 `target` 아래에 산출물이 생성된다.
- 테스트를 실행한 경우 JUnit 테스트가 통과한다.
- 생산 빌드에서는 `exam`, `performance`, local MyBatis, exam mapper 리소스가 제외된다.

## Rollback

- 빌드 산출물만 제거해야 하면 `mvn clean`을 실행한다.
- 코드 변경을 되돌릴 때는 의도한 파일만 대상으로 삼고, 다른 작업자의 변경을 함께 되돌리지 않는다.

## Related Notes

- [[PointHub]]
- [[PointHub Application Structure]]
- [[PointHub Context Pack]]
