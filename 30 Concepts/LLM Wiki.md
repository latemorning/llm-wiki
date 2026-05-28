---
type: concept
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - concept/llm-wiki
---

# LLM Wiki

## Definition

LLM wiki는 사람이 읽는 지식 위키와 LLM에게 전달하는 작업 맥락을 함께 관리하는 문서 구조다.

## Why It Exists

일반 위키는 탐색에는 좋지만 LLM에게 그대로 넘기기에는 길고 산만해지기 쉽다. LLM wiki는 원본 노트와 별도로 짧은 context pack을 유지해서 질문, 코드 수정, 리뷰, 조사 작업에 필요한 맥락을 빠르게 제공한다.

## Pattern

- 원본 지식은 프로젝트, 시스템, 개념, 결정, 런북에 나눠 둔다.
- 근거는 출처 노트에 남긴다.
- LLM 입력용 요약은 context pack으로 만든다.
- context pack에는 작업 목표, 현재 사실, 제약, 관련 파일, 피해야 할 실수를 넣는다.

## Anti-Patterns

- 긴 프로젝트 문서를 그대로 프롬프트에 붙여넣기
- 출처 없는 확정적 문장
- 오래된 정보를 최신 정보처럼 유지하기
- 비밀값과 운영 데이터를 위키에 저장하기

