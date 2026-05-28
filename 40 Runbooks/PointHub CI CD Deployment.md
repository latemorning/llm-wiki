---
type: runbook
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - runbook/pointhub
  - runbook/cicd
  - project/pointhub
---

# PointHub CI CD Deployment

## Goal

PointHub 계열 WAR 산출물을 artifact storage에서 받아 대상 서버에 배포하고, 기존 WAR 백업과 신규 WAR staged copy를 남긴다.

## Preconditions

- target server, host, user, target directory는 Jenkins credential 또는 승인된 설정 저장소에서 주입한다.
- storage account, client id, SSH key, IP, 서버명은 위키에 저장하지 않는다.
- 배포 대상별 service name, app name, environment, artifact 확장자, tag 형식이 확정되어 있어야 한다.

## Steps

1. managed identity 또는 승인된 credential로 artifact storage에 로그인한다.
2. branch/tag 기준으로 배포 대상 artifact 이름을 계산한다.
3. artifact 존재 여부를 먼저 확인하고 없으면 pipeline을 중단한다.
4. target server 목록을 승인된 mapping에서 해석한다.
5. 원격 서버의 배포 staging directory와 backup directory를 만든다.
6. 현재 실행 중인 WAR가 있으면 timestamp가 붙은 이름으로 backup directory에 복사한다.
7. 신규 artifact를 staging directory로 전송한다.
8. 전송된 artifact를 runtime directory의 staged filename으로 복사한다.
9. 필요하면 별도 restart 절차에서 staged WAR를 실제 서비스 파일로 교체한다.

## Verification

- artifact check stage에서 정확한 파일 1개 이상을 찾는다.
- 원격 서버에 backup WAR와 신규 staged WAR가 존재한다.
- 배포 후 `ls -al` 또는 동등한 검증 명령으로 파일 크기와 timestamp를 확인한다.
- restart가 포함된 pipeline이라면 WAS/Tomcat 로그와 health check를 확인한다.

## Rollback

- 신규 WAR 문제가 있으면 timestamp backup 파일을 runtime WAR로 되돌린다.
- SSH 전송 실패 시 runtime WAR를 교체하지 않는다.
- 서버별 병렬 배포 중 일부만 실패하면 성공/실패 서버 목록을 분리해 재처리한다.

## Related Notes

- [[PointHub Runtime and Middleware]]
- [[Tomcat Multi Instance Shutdown]]
- [[PointHub Build and Test]]

## Do Not Store

- 서버 IP, private key, storage account 실제 값, managed identity id
- Jenkins credential id의 secret 내용
- 운영 target directory의 상세 서버별 목록

