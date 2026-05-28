---
type: runbook
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - runbook/safedb
  - project/pointhub
---

# SafeDB Agent Setup

## Goal

PointHub 환경에 SafeDB Agent와 SDK를 설치하고, 보안 파일 권한과 설정 정합성을 확인한다.

## Preconditions

- Agent, SDK, 라이선스 파일은 승인된 경로에서 받아야 한다.
- 인증서, 개인키, 라이선스, properties, XML 원문은 이 위키에 저장하지 않는다.
- 기존 설치본은 삭제하지 않고 `safedb_old` 같은 이름으로 백업한다.

## Steps

1. 서버 역할에 맞는 SafeDB home 경로를 정한다.
2. 기존 설치 디렉터리를 백업한다.
3. 신규 Agent 패키지를 압축 해제한다.
4. `SafeDBMap_config.xml`이 패키지에 없으면 기존 백업본에서 가져오되, `Socket propertyPath`를 현재 설치 경로에 맞춘다.
5. `INISAFENet.properties` 또는 server properties에서 인증서/개인키/로그 경로가 현재 배포 구조와 맞는지 확인한다.
6. Agent별 `agent_id`, emergency mode, 정책 서버 host가 환경에 맞는지 확인한다.
7. 실행 스크립트에 필요한 작업 디렉터리 이동 로직을 추가한다.
8. 소유자와 권한을 최소 권한 기준으로 설정한다.
9. Agent를 기동하고 정책 파일 생성, listen port, 로그를 확인한다.
10. SDK jar는 Maven local repository 또는 프로젝트 extlib 정책에 맞게 설치한다.

## Verification

- 정책 파일이 생성 또는 갱신된다.
- Agent 관련 포트가 listen 상태다.
- 종료 로그에서 memory zero 완료 메시지를 확인한다.
- WAS 기동 시 SafeDB 초기화 오류가 없다.
- `_enc` 컬럼 암호화와 복호화 테스트는 개인값이 아닌 더미 데이터로만 수행한다.

## Rollback

- 신규 Agent 기동 실패 시 백업 디렉터리로 원복한다.
- `SafeDBMap_config.xml` 경로 불일치가 있으면 property path만 수정하고 키/인증 값은 변경하지 않는다.
- 마스터 패스워드 또는 인증 관련 문제는 승인된 운영 절차로만 재설정한다.

## Related Notes

- [[PointHub SafeDB Encryption]]
- [[PointHub Runtime and Middleware]]
- [[PointHub Local Development Environment]]

## Do Not Store

- 인증서, 개인키, 라이선스 파일 내용
- `AUTH password` 값
- 정책 서버 IP/운영 endpoint
- 개인 테스트값, 전화번호, CI, 이름

