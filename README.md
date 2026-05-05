# minseo-toolkit

강민서 개인 Claude Code 툴킷. 어디서든 명령 한 줄로 동일한 작업 환경 복원.

## 🚀 빠른 시작

### 1. 내 툴킷 설치 (Private)
```
/plugin marketplace add approvalsb/minseo-toolkit
/plugin install minseo-toolkit@minseo-toolkit
```

### 2. CLAUDE.md 적용
```bash
cp ~/.claude/plugins/cache/minseo-toolkit/*/CLAUDE-template.md ~/CLAUDE.md
```

### 3. 외부 마켓플레이스/스킬 추가 (아래 섹션 참조)

---

## 📦 포함 내용

### 🤖 개발 Agent 21개 (`agents/`)
analyst, architect, build-fixer, code-reviewer, code-simplifier, critic, debugger, deep-executor, designer, document-specialist, executor, explore, git-master, planner, qa-tester, quality-reviewer, scientist, security-reviewer, test-engineer, verifier, writer

### 🏢 회사 조직도 Agent 25개 (`agents/`)
- **경영진**: strategy, secretary
- **기획본부**: biz-planning, product-planning, service-planning, feature-planning
- **제품본부**: design, ux
- **엔지니어링**: dev, infra, automation, qa, security
- **그로스**: marketing, content, sales
- **운영지원**: data-analytics, cs, finance, legal, audit
- **고객단**: customer-general, customer-startup, customer-enterprise
- **워크플로우**: collaboration-protocol

### ⚡ 슬래시 명령 11개 (`commands/`)
| 명령 | 설명 |
|------|------|
| `/plan-review` | CEO→디자인→엔지니어링 3-step 플랜 리뷰 |
| `/workflow-a` | 신규 사업 런칭 (8단계, 5게이트) |
| `/workflow-b` | 버그/기능 개선 (6단계) |
| `/workflow-c` | 마케팅 캠페인 (5단계) |
| `/workflow-d` | 요금제/가격 변경 (5단계) |
| `/workflow-e` | 고객 피드백 반영 (5단계, 재심사 루프) |
| `/task-review` | nst_tasks 태스크 검토 (3-Phase) |
| `/gap-analysis` | 5축 갭 분석 |
| `/daily-brief` | 엔지니어링 일간 브리프 |
| `/weekly-report` | 전 본부 주간 보고 |
| `/monthly-report` | 전사 월간 경영 보고 |
| `/retro` | 엔지니어링 회고 (git 정량 + 정성) |

### 🛠️ 단일 스킬 4개 (`skills/`)
agent-browser, beautiful-prose, excalidraw, guide-mode

### 📋 워크플로우 정의 (`workflows/`)
A~E 5가지 파이프라인 README

### 📄 CLAUDE.md 템플릿 (`CLAUDE-template.md`)
회사 조직도 + 협업 프로토콜 + 게이트 + 자동 디스패처 전문

---

## 🌐 함께 쓰는 외부 마켓플레이스

### Claude Code 공식/커뮤니티
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

### 도메인 스킬 마켓플레이스 (10개)
```
/plugin marketplace add callstackincubator/agent-skills      # callstack 종합
/plugin marketplace add antonbabenko/terraform-skill         # terraform
/plugin marketplace add CloudAI-X/threejs-skills             # three.js
/plugin marketplace add tinybirdco/tinybird-agent-skills     # tinybird
/plugin marketplace add ibelick/ui-skills                    # UI 컴포넌트
/plugin marketplace add massimodeluisa/recursive-decomposition-skill
/plugin marketplace add remotion-dev/skills                  # remotion
/plugin marketplace add wrsmith108/varlock-claude-skill      # 환경변수 보안
/plugin marketplace add better-auth/skills                   # 인증
/plugin marketplace add neondatabase/agent-skills            # NeonDB
```

---

## 🔌 CLI 도구 (npm 글로벌)

```bash
npm i -g \
  @anthropic-ai/claude-code \
  @openai/codex \
  vercel \
  supabase \
  pm2 \
  firecrawl \
  notebooklm-mcp-server \
  oh-my-claude-sisyphus \
  excalidraw-cli \
  gsd-cli
```

추가로 `brew install`:
```bash
brew install bun node python git ffmpeg gh
brew install --cask obsidian visual-studio-code
```

---

## 🔗 MCP 서버

### 로컬 (mcp.json에 직접 정의)
```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["-y", "figma-developer-mcp", "--figma-api-key", "YOUR_KEY", "--stdio"]
    }
  }
}
```
파일 위치: `~/.claude/mcp.json`

### Claude.ai 데스크톱 앱 통합 (재인증 필요)
새 디바이스에서 Claude.ai 앱 로그인 후 다음 MCP 다시 연결:
- Gmail, Google Calendar, Google Drive
- Slack, Notebooklm
- Firecrawl
- PlayMCP (네이버 검색, 카카오톡, 뉴스)

### Telegram 플러그인 페어링
```
/telegram:access
```

---

## 🔄 새 디바이스 셋업 순서

```bash
# 1. Claude Code 설치 + 로그인
npm i -g @anthropic-ai/claude-code
claude /login

# 2. 내 툴킷 설치
# (Claude Code 안에서)
/plugin marketplace add approvalsb/minseo-toolkit
/plugin install minseo-toolkit@minseo-toolkit

# 3. 외부 마켓플레이스 + 플러그인 (위 섹션의 명령 모두 실행)

# 4. CLAUDE.md 적용
cp ~/.claude/plugins/cache/minseo-toolkit/*/CLAUDE-template.md ~/CLAUDE.md

# 5. CLI 인증
gh auth login
vercel login
supabase login

# 6. MCP 재연결 (Claude.ai 데스크톱 앱)
# 7. /telegram:access 페어링
```

---

## 📝 라이선스

Private. 강민서(Minseo Kang) 개인 사용.

문의: founder@approval-admin.com
