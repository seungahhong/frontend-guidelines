# Dev Workflow Multi-Agent Skills

요구사항 분석 → 계획 → 설계 → 검증 → 구현 → 최적화까지, 소프트웨어 개발 전 과정을 지원하는 Claude Code 스킬 플러그인입니다.

## Skills

### Planning & Design

| Skill | Command | Description |
|-------|---------|-------------|
| **Planner** | `/planner` | 4단계 프로세스(인터뷰 → 조사 → 계획 생성 → 승인)를 통해 실행 가능한 PRD를 작성합니다 |
| **Architecture** | `/architecture` | 시스템 구조, API, 컴포넌트, 데이터 흐름, 기술 선택의 근거를 체계적으로 설계합니다 |
| **Critic** | `/critic` | 설계의 약점, 리스크, 누락 사항을 체계적으로 분석합니다. `/planner`나 `/architecture`와 함께 사용하면 효과적입니다 |
| **Grill Me** | `/grill-me` | 계획이나 설계에 대해 집요하게 질문하여 모호한 부분을 명확히 합니다 |

### Implementation

| Skill | Command | Description |
|-------|---------|-------------|
| **TDD** | `/tdd` | Red-Green-Refactor 루프 기반 테스트 주도 개발을 지원합니다 |

### Quality & Optimization

| Skill | Command | Description |
|-------|---------|-------------|
| **A11y** | `/a11y` | React/JSX 코드의 웹접근성(WAI-ARIA)을 점검하고 개선합니다 |
| **Semantic HTML** | `/semantic-html` | React/JSX 코드의 시맨틱 HTML 태그 사용을 점검하고 개선합니다 |
| **SEO/GEO Optimizer** | `/seo-geo-optimizer` | 전통적 검색엔진과 AI 검색엔진 모두에 대한 최적화를 수행합니다 |

## Agents

스킬을 조합하여 복합적인 작업을 수행하는 서브 에이전트입니다.

| Agent | File | Description |
|-------|------|-------------|
| **Analyst** | `plugins/frontend-develop-guidelines/agents/analyst.md` | grill-me 스킬을 활용하여 요구사항을 체계적으로 분석하고 명세를 도출합니다 |
| **PRD** | `plugins/frontend-develop-guidelines/agents/prd.md` | planner → architecture → critic 루프를 순환하며 완성도 높은 개발 요구사항 정의서를 작성합니다 |
| **Frontend Guidelines** | `plugins/frontend-develop-guidelines/agents/frontend-guidelines.md` | 웹접근성, 시맨틱 HTML, SEO/GEO, TDD 스킬을 조합하여 프론트엔드 개발 가이드라인을 제공합니다 |

## Recommended Workflow

### 스킬 단위 실행

```
/grill-me          # 1. 요구사항 명확화
    ↓
/planner           # 2. 구현 계획 수립 (PRD)
    ↓
/architecture      # 3. 기술 아키텍처 설계
    ↓
/critic            # 4. 설계 검증 및 리스크 분석
    ↓
/tdd               # 5. 테스트 주도 구현
    ↓
/a11y              # 6. 웹접근성 점검
/semantic-html     #    시맨틱 HTML 점검
/seo-geo-optimizer #    SEO/GEO 최적화
```

### 에이전트 기반 자동화

```
Analyst Agent              # 1. 요구사항 분석 (grill-me 활용)
    ↓
PRD Agent                  # 2. PRD 작성 (planner → architecture → critic 루프)
    ↓
Frontend Guidelines Agent  # 3. 프론트엔드 개발 (a11y + semantic-html + seo-geo + tdd)
```

## Installation

Claude Code에서 설치:

```bash
claude plugin add seungahhong/frontend-guidelines
```

설치 후 모든 스킬을 슬래시 커맨드(`/planner`, `/tdd` 등)로 사용할 수 있습니다.

## Project Structure

```
.claude-plugin/
  marketplace.json                                       # 마켓플레이스 리스팅 정보
plugins/
  frontend-develop-guidelines/                           # 플러그인 루트
    .calude-plugin/
      plugin.json                                        # 플러그인 메타데이터
    skills/
      planner/                                           # 계획 수립 (+ references/)
      architecture/                                      # 아키텍처 설계
      critic/                                            # 설계 검증
      grill-me/                                          # 인터뷰
      tdd/                                               # 테스트 주도 개발 (+ references/)
      a11y/                                              # 웹접근성 점검 (+ references/)
      semantic-html/                                     # 시맨틱 HTML 점검
      seo-geo-optimizer/                                 # SEO/GEO 최적화 (+ references/)
    agents/
      analyst.md                                         # 요구사항 분석 서브 에이전트
      prd.md                                             # PRD 작성 서브 에이전트
      frontend-guidelines.md                             # 프론트엔드 가이드라인 서브 에이전트
```

## License

MIT
