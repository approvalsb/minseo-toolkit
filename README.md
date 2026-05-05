# minseo-toolkit

강민서 개인 Claude Code 툴킷. 어디서든 명령 한 줄로 동일한 작업 환경 복원.

## 설치

```
/plugin marketplace add approvalsb/minseo-toolkit
/plugin install minseo-toolkit@minseo-toolkit
```

## 포함

### 1. 개발 Agent 21개 (`agents/`)
- analyst, architect, build-fixer, code-reviewer, code-simplifier, critic
- debugger, deep-executor, designer, document-specialist, executor, explore
- git-master, planner, qa-tester, quality-reviewer, scientist, security-reviewer
- test-engineer, verifier, writer

### 2. 회사 조직도 Agent 24개 (`agents/`)
- 경영진: strategy, secretary
- 기획본부: biz-planning, product-planning, service-planning, feature-planning
- 제품본부: design, ux
- 엔지니어링: dev, infra, automation, qa, security
- 그로스: marketing, content, sales
- 운영지원: data-analytics, cs, finance, legal, audit
- 고객단: customer-general, customer-startup, customer-enterprise

### 3. 워크플로우 정의 (`workflows/`)
- 신규 사업 / 버그 수정 / 마케팅 / 요금제 / 고객 피드백 5가지 파이프라인

### 4. CLAUDE.md 템플릿 (`CLAUDE-template.md`)
회사 조직도 정의 + 협업 프로토콜 + 게이트 + 자동 디스패처. 새 환경에 `~/CLAUDE.md`로 복사 후 사용.

### 5. 단일 스킬 4개 (`skills/`)
- agent-browser
- beautiful-prose
- excalidraw
- guide-mode

## 함께 쓰는 외부 마켓플레이스 (별도 install 필요)

```
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin marketplace add anthropics/claude-plugins-official
/plugin marketplace add anthropics/claude-code
/plugin marketplace add f/prompts.chat
/plugin marketplace add kepano/obsidian-skills

/plugin install oh-my-claudecode@omc
/plugin install frontend-design@claude-plugins-official
/plugin install telegram@claude-plugins-official
```

## 새 디바이스 셋업 후

1. 위 install 명령 실행
2. `CLAUDE-template.md` → `~/CLAUDE.md`로 복사
3. `/login`, `gh auth login`, `vercel login`, `supabase login`
4. Claude.ai MCP 재연결 (Gmail, Slack, Calendar 등)

## 라이선스

Private. 강민서 개인 사용.
