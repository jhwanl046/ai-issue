# 포스트모템 (Postmortem) — 가상 문제 상황

## Incident: variance() NaN 전파로 가설검정 전체 실패
- **심각도:** SEV-2 (핵심 통계 기능 불가)
- **발생:** 2026-11-19 14:00 KST · **해결:** 2026-11-19 18:30 KST (≈4.5h)
- **영향:** 가설검정/회귀 모듈 사용자 100% 실패, CI nightly red

### Summary (STAR)
- **S (Situation):** v0.2.0 릴리스 직후 대용량 CSV(>10⁶행)에서 `variance()`가 `NaN`을 반환, Welch t-test/회귀가 연쇄 실패.
- **T (Task):** 원인 규명 + 핫픽스 릴리스 + 재발 방지.
- **A (Action):** 입력 정규화(δ 스케일링)와 Welford 재적용, NaN/Inf 입력 가드 추가, 가설검정 입력 검증 강화, 회귀 테스트 추가.
- **R (Result):** 핫픽스 v0.2.1 배포, 대용량 입력 테스트 통과, SLA 내 복구.

### Root Cause
- 단순 합/제곱합 방식: `Σx² - (Σx)²/n` 소거 오차(catastrophic cancellation) → 큰 N에서 음수/NaN.
- 가설검정 모듈이 `NaN` 분산을 propagate (입력 검증 부재).

### What / What / How
- **What (문제):** 대용량 입력에서 분산 NaN → 다운스트림 전면 실패.
- **What (원인):** 수치 불안정 공식 + 입력 검증 미비.
- **How (조치/재발 방지):**
  1. Welford 알고리즘 채택 (Day 3 학습 적용)
  2. `math.isfinite` 가드 + 명시적 `ValueError`
  3. 10⁶행 이상 입력에 대한 스트레스 테스트 추가 (CI)
  4. 릴리스 전 수치 회귀(numerical regression) 체크리스트에 포함

### Action Items
| # | 항목 | 담당 | 기한 |
|---|------|------|------|
| 1 | Welford 전 함수 적용 | stats | 2026-11-20 |
| 2 | 입력 가드 공통 유틸 | core | 2026-11-20 |
| 3 | 스트레스 테스트 CI 편입 | CI | 2026-11-21 |
| 4 | 릴리스 체크리스트 갱신 | docs | 2026-11-21 |
