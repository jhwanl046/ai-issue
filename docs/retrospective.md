# 스프린트 회고 (Sprint Retrospective)

## Sprint 1 — Week 1: Core implementation (Issues #2~#8)

### What happened (사실)
- 프로젝트 스캐폴딩, 기초 통계, 데이터 로더, 타입 추론, pytest, 문서, 부동소수점 결함 수정까지 #2~#8 완료 (7개 이슈).
- 분산 계산에서 큰 수 오차 발견 → Welford 적용으로 해결.

### What went well / What didn't (잘한 점 / 아쉬운 점)
- **잘:** 이슈 단위로 브랜치/PR 분리 → 리뷰·회귀 추적 용이.
- **아쉬움:** 초기 타입 추론 규칙이 모호해 데이터 로더 재작업 1회 발생.

### How to improve (개선)
- 통계 함수 계약(입력/출력/에러)을 스프린트 시작에 ADR로 고정.
- 타입 추론 규칙을 작은 명세 문서로 선행 작성 후 구현.

## Sprint 2 — Week 2: Analysis & visualization (Issues #9~#13)

### What happened (사실)
- 가설검정(t/Welch/χ²), 상관/회귀, 시각화 유틸, CI, 샘플 데이터/노트북 완료 (5개 이슈).
- matplotlib 기본 스타일 가독성 이슈 → seaborn 테마로 개선.
- CI는 ruff + pytest matrix 구성 완료.

### What went well / What didn't
- **잘:** CI 도입 후 포맷/린트 회귀 0건. 시각화 재사용 유틸로 노트북 코드량 감소.
- **아쉬움:** 가설검정 파라미터(`equal_var`) 기본값에 대한 문서화가 늦어 사용자 혼란 발생 가능.

### How to improve
- 릴리스 전 API 문서 자동 생성(mkdocs) 파이프라인 추가.
- "배포됨"(Issue #1) 릴리스 체크리스트: 버전 bump → 태그 → 릴리스 노트 → PyPI 업로드.
