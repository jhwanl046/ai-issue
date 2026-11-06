# TIL — 파이썬 통계 프로젝트 (14일)

> 프로젝트: `jhwanl046/ai-issue` (Week 1: 기초 구현 / Week 2: 분석 & 시각화)

## Day 1 — 프로젝트 스캐폴딩 (Issue #2)
- **What:** src 레이아웃 + `pyproject.toml`로 패키지/의존성/엔트리포인트 통합이 편하다.
- **How:** `src/`, `tests/`, `docs/` 분리하고 ruff/pytest 설정을 pyproject에 집중.

## Day 2 — 기초 기술통계 (Issue #3)
- **What:** mean/median/mode/variance/std는 입력 검증(빈 리스트, 상수)부터 설계해야 한다.
- **How:** `StatisticsError` 등으로 엣지 케이스를 명시적 처리.

## Day 3 — 수치 안정성 (Issue #7)
- **What:** 단순 합/제곱합으로 분산을 계산하면 큰 수에서 오차가 누적된다.
- **How:** Welford 알고리즘으로 한 패스에서 안정적인 분산/표준편차 계산.

## Day 4 — CSV/JSON 데이터 로더 (Issue #4)
- **What:** pandas 의존 없이 csv/json 표준 라이브러리만으로도 충분한 로더가 가능하다.
- **How:** `csv.DictReader`, `json.load` + 제너레이터로 메모리 효율.

## Day 5 — 타입 추론 (Issue #4)
- **What:** 컬럼 타입(int/float/str) 추론 시 "NA", "", "null" 처리 규칙이 중요하다.
- **How:** 샘플 기반 추론 후 실패 시 str 폴백하는 보수적 전략.

## Day 6 — pytest & 커버리지 (Issue #5)
- **What:** 픽스처로 데이터/임시 파일을 격리하면 테스트가 결정적이 된다.
- **How:** `pytest --cov` + `pyproject`의 fail-under로 품질 게이트.

## Day 7 — Docstring/Type Hints (Issue #8)
- **What:** NumPy/Google 스타일 docstring은 IDE 툴팁과 자동 문서 생성에 유리하다.
- **How:** 모든 공개 함수에 타입 힌트 + 예제 docstring 추가.

## Day 8 — 문서화 (Issue #6)
- **What:** README는 설치→빠른시작→API 한눈에 뷰 순서가 이탈을 줄인다.
- **How:** 빠른 예제 + 뱃지(CI/coverage)로 신뢰 형성.

## Day 9 — 가설검정 (Issue #9)
- **What:** t-검정은 등분산 가정 여부에 따라 pooled/Welch를 분기해야 한다.
- **How:** `equal_var` 파라미터 + degrees of freedom 계산 명시.

## Day 10 — 상관/회귀 (Issue #10)
- **What:** Pearson은 선형, Spearman은 순위 기반 — 데이터 특성에 맞게 선택.
- **How:** OLS 기울기/절편과 R²를 함께 반환하고 결측값 정책 문서화.

## Day 11 — 시각화 (Issue #11)
- **What:** matplotlib 기본 스타일은 투박하므로 seaborn 테마를 적용하면 가독성이 크게 향상.
- **How:** figure/axes 유틸 함수로 재사용 가능한 플롯 빌더 구성.

## Day 12 — GitHub Actions CI (Issue #12)
- **What:** CI는 로컬에서 통과시킨 명령과 동일해야 재현성이 높다.
- **How:** ruff check + pytest를 matrix(Python 버전)로 실행.

## Day 13 — 샘플 데이터/노트북 (Issue #13)
- **What:** 작은 내장 데이터셋으로 튜토리얼을 만들면 온보딩 비용이 낮아진다.
- **How:** datasets/ 디렉터리 + Jupyter 노트북에 단계별 예시.

## Day 14 — 배포 (Issue #1)
- **What:** "배포됨" 이슈는 릴리스 체크리스트(버전 bump, 태그, 노트)로 관리하면 누락이 적다.
- **How:** GitHub Release + 태그(v0.x) 생성하고 변경 로그 자동화.
