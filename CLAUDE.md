# Frontend Guidelines - Dev Workflow Multi-Agent Skills

소프트웨어 개발 전 과정을 지원하는 Claude Code 스킬 플러그인.

## Project Structure

```
.claude-plugin/                                          # 마켓플레이스 등록 메타데이터
  marketplace.json                                       # 리스팅 정보 (owner, metadata, plugins)
plugins/
  frontend-develop-guidelines/                           # 플러그인 루트
    .claude-plugin/
      plugin.json                                        # 플러그인 메타데이터 (이름, 버전, 키워드, 스킬/에이전트 경로)
    commands/                                            # 커스텀 커맨드 디렉토리
      orchestrator.md                                    # 전체 워크플로우 오케스트레이터 (analyst → prd → frontend-guidelines)
    skills/                                              # 스킬 정의 디렉토리
      planner/                                           # 계획 수립 에이전트 (+ references/)
      architecture/                                      # 아키텍처 설계 에이전트
      critic/                                            # 설계 검증 에이전트
      grill-me/                                          # 인터뷰 에이전트
      tdd/                                               # 테스트 주도 개발 (+ references/)
      a11y/                                              # 웹접근성 점검 (+ references/)
      semantic-html/                                     # 시맨틱 HTML 점검
      seo-geo-optimizer/                                 # SEO/GEO 최적화 (+ references/)
    agents/                                              # 서브 에이전트 정의 디렉토리
      analyst.md                                         # 요구사항 분석 (grill-me 활용)
      prd.md                                             # PRD 작성 (planner → architecture → critic 루프)
      frontend-guidelines.md                             # 프론트엔드 가이드라인 (a11y + semantic-html + seo-geo + tdd)
```

## Skills

| Skill | Command | Description |
|-------|---------|-------------|
| Planner | `/planner` | 인터뷰 → 조사 → 계획 생성 → 승인 4단계 PRD 작성 |
| Architecture | `/architecture` | 시스템 구조, API, 데이터 흐름 설계 |
| Critic | `/critic` | 설계의 약점, 리스크, 누락 사항 분석 |
| Grill Me | `/grill-me` | 요구사항 명확화를 위한 집요한 질문 |
| TDD | `/tdd` | Red-Green-Refactor 루프 기반 개발 |
| A11y | `/a11y` | WAI-ARIA 기반 웹접근성 점검/개선 |
| Semantic HTML | `/semantic-html` | 시맨틱 태그 사용 점검/개선 |
| SEO/GEO | `/seo-geo-optimizer` | 검색엔진 + AI 검색 최적화 |

## Commands

| Command | File | Description |
|---------|------|-------------|
| Orchestrator | `plugins/frontend-develop-guidelines/commands/orchestrator.md` | analyst → prd → frontend-guidelines 순차 실행 후 통합 리포트 생성 |

## Agents

| Agent | File | Description |
|-------|------|-------------|
| Analyst | `plugins/frontend-develop-guidelines/agents/analyst.md` | grill-me 스킬로 요구사항 분석 및 명세 도출 |
| PRD | `plugins/frontend-develop-guidelines/agents/prd.md` | planner → architecture → critic 루프로 개발 요구사항 정의서 작성 |
| Frontend Guidelines | `plugins/frontend-develop-guidelines/agents/frontend-guidelines.md` | a11y, semantic-html, seo-geo, tdd 스킬 조합으로 프론트엔드 가이드라인 제공 |

## Conventions

- 각 스킬은 `plugins/frontend-develop-guidelines/skills/<skill-name>/SKILL.md`에 정의
- 각 에이전트는 `plugins/frontend-develop-guidelines/agents/<agent-name>.md`에 정의
- 참고 자료는 `plugins/frontend-develop-guidelines/skills/<skill-name>/references/` 하위에 배치
- 스킬/에이전트 설명은 한국어로 작성
- 스킬 간 교차 참조 시 상대 경로 사용 (예: `../a11y/SKILL.md`)
