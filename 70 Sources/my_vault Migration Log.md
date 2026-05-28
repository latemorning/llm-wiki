---
type: source
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - source/migration
  - project/pointhub
---

# my_vault Migration Log

## Scope

`/Users/harry/obsidianVaults/my_vault`에서 개발 위키에 필요한 업무/기술 지식만 이관했다. 개인 메모와 원문 민감 파일은 그대로 복사하지 않았다.

## Handling Rules

- 개인 영역, 주식, 취미, 이메일 초안은 개발 위키로 이관하지 않는다.
- `.obsidian`, 플러그인, 개인 vault 설정은 이관하지 않는다.
- properties, PRD DDL, Java 유틸리티, API 테스트값은 원문 복사하지 않고 요약 또는 절차만 남긴다.
- IP, 계정, 경로, 토큰, 키, 전화번호, CI, 개인명, 암호문은 새 노트에 저장하지 않는다.
- 원문을 마스킹 요약으로 대체한 파일은 삭제 대상에 포함한다.

## Migrated Notes

- [[PointHub SafeDB Encryption]]
- [[PointHub Runtime and Middleware]]
- [[PointHub Card Cancel C160]]
- [[PointHub Local Development Environment]]
- [[PointHub Local DB Migration]]
- [[SafeDB Agent Setup]]
- [[Tomcat Multi Instance Shutdown]]
- [[PointHub CI CD Deployment]]
- [[0002 Standardize PointHub Runtime Stack]]

## Source Files Summarized And Safe To Delete

- `1_Projects/Pointhub_암호화/변환순서.md`
- `1_Projects/Pointhub_암호화/30_phub/311_상속형 -> 선언형 정리.md`
- `1_Projects/Pointhub_암호화/30_phub/312_상속형 <-> 선언형 변환.md`
- `1_Projects/Pointhub_암호화/30_phub/313_포인트허브 프로젝트개선사항.md`
- `1_Projects/Pointhub_암호화/30_phub/서버목록.md`
- `1_Projects/Pointhub_암호화/PG_약관_포인트_API_테스트값.md`
- `1_Projects/Pointhub_암호화/UserTokenInserterApp.java`
- `1_Projects/Pointhub_암호화/UserTokenInserterApp 1.java`
- `1_Projects/Pointhub_암호화/INISAFENet_Server.properties`
- `1_Projects/Pointhub_암호화/INISAFENet_Server 1.properties`
- `1_Projects/Pointhub_암호화/[PRD]DDL_SCHEMA_pointhub_phub_260108.sql`
- `1_Projects/Pointhub_암호화/[PRD]DDL_SCHEMA_pointhub_phub_260108 1.sql`
- `1_Projects/공통/서버별_파라미터정리.md`
- `1_Projects/공통/서버별_파라미터정리2.md`
- `1_Projects/공통/미들웨어_파라미터_적용요청_이메일.md`
- `1_Projects/공통/카드취소_배치처리/Todo.md`
- `1_Projects/공통/카드취소_배치처리/상세설계.md`
- `1_Projects/로컬개발환경/서버구성계획.md`
- `1_Projects/로컬개발환경/서버구성계획_DB.md`
- `1_Projects/로컬개발환경/TB_포트관리.md`
- `1_Projects/로컬개발환경/CLAUDE.md`
- `3_Resources/기술/데이터베이스/SafeDB/SafeDB_가이드.md`
- `3_Resources/기술/데이터베이스/SafeDB/SafeDB_SDK_maven_install.md`
- `3_Resources/기술/데이터베이스/SafeDB/TB_서버_설치_정리.md`
- `3_Resources/기술/데이터베이스/DB관련/포인트허브스크립트.md`
- `3_Resources/문제해결/Tomcat 다중 인스턴스 Shutdown 문제 분석 및 해결.md`
- `2_Areas/업무/CI_CD/CD.md`
- `GEMINI.md`
- `CLAUDE.md`
- `AGENTS.md`

## Sensitive Files Redacted And Safe To Delete

- `무제.md`: API 테스트값, 암호문, 개인명/전화번호성 데이터가 포함되어 원문은 이관하지 않았다.
- `2_Areas/업무/08_playground/apps/auto-post.md`: Telegram bot token과 user id가 포함되어 원문은 이관하지 않았다.
- `2_Areas/업무/08_playground/apps/auto-report.md`: Google Sheet id와 외부 연동 설정 질문이 포함되어 원문은 이관하지 않았다.
- `PG_약관_포인트_API_테스트값.md`: 개인 테스트값과 암호문이 포함되어 원문은 이관하지 않았다.
- SafeDB properties와 PRD DDL 파일: 운영 구성과 schema 원문이 포함되어 원문은 이관하지 않았다.

## Not Migrated And Kept In Source

- `2_Areas/개인/**`
- `2_Areas/개인/주식.md`
- `Email/**`
- `.obsidian/**`
- `.obsidian.vimrc`
- 취미/개인성 루트 메모
- 기술 일반 자료 중 PointHub/개발 위키와 직접 관련 없는 자료

## Security Follow Up

- Source vault에 Telegram bot token으로 보이는 값이 있었다. 새 위키에는 저장하지 않았고, 해당 token은 회전 또는 폐기해야 한다.
- API 테스트값에는 개인명, 전화번호, CI 또는 암호문으로 보이는 값이 있었다. 새 위키에는 저장하지 않았다.
