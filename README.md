# minseo-toolkit

빌더민서가 매일 쓰는 Claude Code 툴킷. 강의에서 본 회사 조직도형 에이전트 시스템과 5종 워크플로우를 한 줄 명령으로 본인 PC에 설치합니다.

> **빌더민서 AI 코딩 강의 수강생용 공개판.** 강의에서 시연한 `@개발`, `@디자인`, `@고객단`, `@워크플로우A~E` 등을 그대로 사용할 수 있게 패키징한 Claude Code 플러그인입니다.

---

## 🚀 설치 (1분)

Claude Code가 깔려 있다는 가정 하에 — 깔려 있지 않으면 [강의 환경 점검 가이드](https://lecture02-review-deploy.vercel.app/setup) 먼저.

```
/plugin marketplace add approvalsb/minseo-toolkit
/plugin install minseo-toolkit@minseo-toolkit
```

설치 후 Claude Code 재시작. 슬래시(`/`) 누르면 `/plan-review`, `/workflow-a` 같은 명령이 자동완성에 뜨면 성공.

### CLAUDE.md 같이 적용 (선택)
회사 조직도 / 협업 프로토콜 / 게이트 시스템 전문이 적힌 CLAUDE.md 템플릿을 본인 홈 디렉토리에 복사:

```bash
# Mac/Linux
cp ~/.claude/plugins/cache/minseo-toolkit/*/CLAUDE-template.md ~/CLAUDE.md
```

```powershell
# Windows PowerShell
Copy-Item "$env:USERPROFILE\.claude\plugins\cache\minseo-toolkit\*\CLAUDE-template.md" "$env:USERPROFILE\CLAUDE.md"
```

이 파일이 있으면 Claude Code가 모든 프로젝트에서 자동으로 읽고 부서 소환·워크플로우·게이트 규칙을 따릅니다.

---

## 📦 안에 들어있는 것

### 🤖 개발 에이전트 21개 (`agents/`)
표준 코딩 작업용 — `analyst`, `architect`, `build-fixer`, `code-reviewer`, `code-simplifier`, `critic`, `debugger`, `deep-executor`, `designer`, `document-specialist`, `executor`, `explore`, `git-master`, `planner`, `qa-tester`, `quality-reviewer`, `scientist`, `security-reviewer`, `test-engineer`, `verifier`, `writer`

### 🏢 회사 조직도 에이전트 25개 (`agents/`)
1인 빌더가 7본부 24부서로 운영하는 가상 회사 시스템.

| 본부 | 부서 |
|------|------|
| **경영진** | strategy, secretary |
| **기획** | biz-planning, product-planning, service-planning, feature-planning |
| **제품** | design, ux |
| **엔지니어링** | dev, infra, automation, qa, security |
| **그로스** | marketing, content, sales |
| **운영지원** | data-analytics, cs, finance, legal, audit |
| **고객단** | customer-general, customer-startup, customer-enterprise |

`@개발`, `@디자인`, `@법무`, `@고객단` 같은 키워드로 호출.

### ⚡ 슬래시 명령 12개 (`commands/`)

| 명령 | 설명 |
|------|------|
| `/plan-review` | CEO→디자인→엔지니어링 3-step 플랜 리뷰 |
| `/workflow-a` | 신규 사업 런칭 (8단계, 5게이트) |
| `/workflow-b` | 버그/기능 개선 (6단계) |
| `/workflow-c` | 마케팅 캠페인 (5단계) |
| `/workflow-d` | 요금제/가격 변경 (5단계) |
| `/workflow-e` | 고객 피드백 반영 (재심사 루프) |
| `/task-review` | 태스크 자동 팀 배정 → 3-Phase 검토 |
| `/gap-analysis` | 5축 갭(누락) 분석 |
| `/daily-brief` | 엔지니어링 일간 브리프 |
| `/weekly-report` | 전 본부 주간 보고 |
| `/monthly-report` | 전사 월간 경영 보고 |
| `/retro` | 엔지니어링 회고 (git 정량 + 정성) |

### 🛠️ 단일 스킬 4개 (`skills/`)
`agent-browser` (브라우저 자동화), `beautiful-prose` (글쓰기 스타일 가이드), `excalidraw` (아키텍처 다이어그램), `guide-mode` (UI 분석 오버레이)

### 📄 CLAUDE-template.md
회사 조직도 + 협업 프로토콜 + 5종 워크플로우 정의 + 자동 디스패처 + Gap 분석 루프 — 약 1100줄.

---

## 🎓 강의 수강생을 위한 추천 사용 흐름

처음에는 **그대로 쓰지 마세요**. 강의 2강 끝나고 본인 MVP 1개를 빈 폴더에서 배포까지 끝낸 다음, 3강에서 본격 적용하기 시작하는 게 정공법입니다.

### 1주차 (지금)
- 설치만 해두기 (`/plugin install`)
- `/plan-review` 한 번만 본인 MVP 기획서로 돌려보기

### 2주차
- CLAUDE-template.md를 본인 회사/프로젝트에 맞게 부서명 한 번 정리
- `@개발 @디자인` 식으로 부서 소환 익히기

### 3주차
- `/workflow-b`로 본인 MVP 버그 1건 처리해보기
- 자기 워크플로에 안 맞는 부서/단계는 과감히 삭제

### 4주차+
- 본인만의 부서/명령 추가 (`agents/*.md`, `commands/*.md` 신규 생성)

---

## ⚠️ 사용 시 주의

- **이건 강민서 1인 빌더 환경에 최적화된 툴킷입니다.** 본인 환경/팀 구성/업종에 맞게 부서명·워크플로우 단계·게이트 기준을 자유롭게 수정하세요. 그대로 쓰면 본인 작업 흐름과 맞지 않을 수 있습니다.
- **부서 에이전트는 결정권자가 아닙니다.** `@법무` 의견은 진짜 법률 자문이 아니고, `@고객단` 점수는 진짜 사용자 검증이 아닙니다. 빠른 사고 정리용 도구로 보세요.
- **Workflow A~E도 강제가 아닙니다.** 핵심 가치는 "팀 간 핸드오프 흐름을 코드로 명시화한 것" 입니다. 본인 회사에서는 다른 흐름이 맞을 수 있습니다.

---

## 🔄 함께 쓰면 좋은 것

```
# Claude Code 메인 라이브러리 (강의에서도 사용)
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode@omc

# Vercel / Frontend Design / Telegram (Anthropic 공식)
/plugin marketplace add anthropics/claude-plugins-official
/plugin install vercel@claude-plugins-official
/plugin install frontend-design@claude-plugins-official
/plugin install telegram@claude-plugins-official
```

---

## 🔗 관련 자료

- 빌더민서 AI 코딩 강의 2강 자료실: https://minseo-ai-lecture-02.vercel.app
- 2강 복습 패키지: https://lecture02-review-deploy.vercel.app
- MVP 보일러플레이트: https://github.com/approvalsb/minseo-mvp-boilerplate

---

## 📝 라이선스

MIT License. 자유롭게 fork·수정·재배포 가능.

문의: founder@approval-admin.com
