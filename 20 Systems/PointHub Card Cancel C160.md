---
type: system
status: active
created: 2026-05-28
updated: 2026-05-28
tags:
  - system/pointhub
  - project/pointhub
---

# PointHub Card Cancel C160

## Purpose

카드포인트 결제 실패 건을 조회하고 선택 건에 C160 수동 보정 값을 일괄 반영하는 기능을 정리한다.

## Responsibilities

- 실패 거래만 조회하도록 기존 카드포인트 전환 조회 로직을 재사용한다.
- 화면에서는 검색, 목록, 체크박스 선택, C160 처리만 제공한다.
- 선택 행은 JSON 배열로 컨트롤러에 전달한다.
- 서버는 클라이언트가 보낸 보정 값을 신뢰하지 않고, `regSource`별 서버 고정 매핑 값으로 덮어쓴다.
- DB 업데이트 대상은 `point_hub_swap_hist` 단일 테이블이다.

## Inputs

- 조회 조건: 거래번호, 허브 거래번호, 승인번호, 조회일자, 소스 구분, 페이지
- 선택 행 JSON: 거래 식별자, 원거래 식별자, 소스, 포인트, 응답 코드 등
- `regSource`별 C160 고정값 매핑

## Outputs

- 실패 거래 목록
- 선택 건의 C160 보정 업데이트
- 처리 결과 flash 메시지와 목록 리다이렉트

## Dependencies

- `clipcms`
- `cardpoint_fail_list.jsp`
- `Clip_3_0_CMSController`
- `Clip_3_0_ServiceImpl`
- `Clip_3_0_DAOImpl`
- `clip_3_0_mapper.xml`
- MyBatis `clip30.updatePointHubSwapHistC160`

## Failure Modes

- `selectedRowsJson` 형식 오류나 빈 배열은 처리하지 않고 오류로 되돌려야 한다.
- `regSource`가 서버 매핑에 없으면 임의 보정이 발생하지 않도록 중단해야 한다.
- 명시적 transaction이 없으면 루프 중 일부 행만 반영될 수 있다.
- 조회 목록에 여러 소스가 보이더라도 실제 UPDATE는 허브 스왑 이력만 대상으로 한다.

## Related Notes

- [[PointHub]]
- [[PointHub Runtime and Middleware]]
- [[PointHub Context Pack]]

## Needs Verification

- 현재 운영에 반영된 카드사별 `regSource` 고정 매핑 목록
- batch update의 transaction 정책

