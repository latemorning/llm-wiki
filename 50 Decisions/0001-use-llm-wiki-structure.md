---
type: decision
status: accepted
created: 2026-05-28
updated: 2026-05-28
tags:
  - decision/wiki
---

# 0001 Use LLM Wiki Structure

## Context

개발 지식이 프로젝트 문서 하나에 모이면 사람이 읽기에는 길어지고, LLM에게 전달하기에는 불필요한 내용이 많아진다.

## Decision

이 vault는 프로젝트, 시스템, 개념, 런북, 결정, 프롬프트, 출처, context pack을 분리해서 관리한다.

## Consequences

- 프로젝트별 진입점이 명확해진다.
- LLM에게 전달할 맥락을 짧게 유지할 수 있다.
- 같은 정보가 여러 곳에 중복될 수 있으므로 context pack은 원본 노트 링크를 포함해야 한다.

