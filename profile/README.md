# Holdings Lab

정책 이벤트와 자산 반응의 연결을 통해, 투자 행동보다 **투자 학습**에 집중하는 금융 학습 시스템을 만듭니다.

## What We Solve

- 금융 정보는 많지만, 뉴스가 내 자산에 미치는 영향을 이해하기 어렵습니다.
- 초보 투자자는 정보 해석 부담, 낮은 초기 보상, 학습 동기 저하로 이탈하기 쉽습니다.
- 기존 서비스는 거래/요약 중심이라 학습 관점의 인사이트가 부족합니다.

## Core Features

- **방향성 예측**: 정책 이벤트 이후 주요 지수/ETF의 상승·하락 확률 제공
- **변동성 예측**: 변동성 급증 가능성을 제시해 리스크 학습 지원
- **자산 민감도 분석**: 이벤트별 민감 자산을 히트맵/랭킹으로 시각화

## Technical Approach

- LLM은 주가를 직접 예측하지 않고 정책/뉴스 텍스트를 **정형 피처(JSON)** 로 추출
- 예측은 **XGBoost / LightGBM** 기반으로 수행해 안정성과 설명 가능성 확보
- 데이터 파이프라인은 **PostgreSQL(JSONB) + FastAPI** 로 구성

## Evaluation Principle

- 단순 정확도 대신 **클래스별 F1-score** 중심으로 평가
- 상승/하락 불균형에서 특히 하락장 탐지 성능을 별도 점검

## Goal

3개월 내 검증 가능한 MVP를 구축해, 사용자가 시장 이벤트의 원인-결과 구조를 이해하도록 돕는 정책 이벤트 기반 금융 학습 플랫폼을 구현합니다.

## Team

- 엄지용 (UI/UX, Feature 설계)
- 이석호 (데이터 수집, DB 관리)
- 이찬준 (모델링, ETF 데이터)
- 함민식 (백엔드, API)
  
# 📝 Commit Convention

[Conventional Commits](https://www.conventionalcommits.org/) 기반 커밋 규칙.
PR 머지 / changelog 자동화.

<br>

## 한 줄 요약

```
<type>(<scope>): <subject>

<body>

<footer>
```

- `type`, `subject`만 필수, 나머지는 선택
- 각 블록 사이는 **빈 줄 한 줄**로 구분

<br>

## Type

| Type       | 언제 쓰는데?                                     |
| ---------- | ------------------------------------------------ |
| `feat`     | 새 기능 추가                                     |
| `fix`      | 버그 수정                                        |
| `docs`     | 문서만 수정 (README, 주석 등)                    |
| `style`    | 포맷팅, 세미콜론 같은 것만 (동작 변경 X)         |
| `refactor` | 기능 그대로 두고 코드만 갈아엎기                 |
| `perf`     | 성능 개선                                        |
| `test`     | 테스트 추가/수정                                 |
| `build`    | 빌드/의존성 (npm, pip, gradle 등)                |
| `ci`       | CI 설정 (GitHub Actions 등)                      |
| `chore`    | 그 외 잡일                                       |
| `revert`   | 이전 커밋 되돌리기                               |

<br>

## Subject 쓸 때 규칙

- **50자 이내**
- **명령문**으로 — `add`, `fix`, `remove` (✅)  /  `added`, `fixing` (❌)
- **마침표 금지**
- 영문은 소문자로 시작 (한글이면 그냥 자연스럽게)

```
✅ feat(auth): add OAuth2 login
❌ feat(auth): Added OAuth2 login.
```

<br>

## Body / Footer

**Body** — "뭘 했는지" 적기. 한 줄 72자 정도에서 끊기.

**Footer** — 이슈 연결 / Breaking Change 표시

```
Closes #123
Fixes #456
Refs #789
```

호환성 깨지는 변경은 `!` 붙이거나 footer에 명시:

```
feat(api)!: change getUser to async

BREAKING CHANGE: 기존 동기 호출부 전부 await 붙여야 함
```

<br>

## Scope 예시

프로젝트 구조 따라 자유롭게.

```
feat(auth): ...
fix(api): ...
refactor(model): ...
docs(readme): ...
```

<br>

## 실제 예시

**가장 단순:**
```
fix: typo in README
```

**scope 포함:**
```
feat(auth): add Google OAuth2 login
```

**본문까지:**
```
refactor(parser): split tokenizer into separate module

parser.ts 가 1000줄 넘어가서 가독성 망함.
토크나이저 분리해서 단위 테스트 쉽게 작성할 수 있게 함.

Refs #102
```

**ML 프로젝트 예시:**
```
feat(model): add FashionMNIST baseline CNN

Conv2d → ReLU → MaxPool → FC 구조 baseline.
test accuracy 89.4%.

Refs #5
```

<br>

## 권장사항

- **커밋 1개 = 변경 1개.** 섞이면 `git add -p` 로 쪼개기
- **WIP 커밋 금지** (어쩔 수 없으면 머지 전 squash)
- PR을 **Squash and merge** 로 머지하면 PR 제목이 곧 커밋이 되니까, **PR 제목도 같은 컨벤션** 으로 쓰기

<br>

## 치트시트 🧾

```
feat:     기능 추가
fix:      버그 수정
docs:     문서
style:    포맷팅
refactor: 리팩터링
perf:     성능
test:     테스트
build:    빌드/의존성
ci:       CI
chore:    잡일
revert:   되돌리기
```

```
<type>(<scope>): <subject>   ← 50자, 명령문, 마침표 ❌

<body>                       ← "왜" 했는지, 72자 줄바꿈

<footer>                     ← Closes #123 / BREAKING CHANGE
```
