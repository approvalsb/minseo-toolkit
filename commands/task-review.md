---
description: nst_tasks 태스크를 자동 팀 배정 → 3-Phase 검토 (논의 → 보고 → 실행 승인)
argument-hint: [task ID 예: NST-001]
---

# 태스크 검토

대상: $ARGUMENTS

## 처리 흐름 (3-Phase)

### PHASE 1: 팀 내부 작업
1. 태스크의 department/title/description 기반으로 관련 팀 자동 식별
2. 주담당 팀이 먼저 분석 → 자동 참여 팀이 크로스 리뷰
3. 각 팀 피드백을 nst_tasks.feedback에 기록

### PHASE 2: 팀 간 교차 검토
4. 주담당 팀 결론 + 참여 팀 피드백 종합
5. 이견 있으면 팀 간 자체 조율
6. 합의된 실행 방안 정리

### PHASE 3: 사용자 보고 및 실행 승인 요청
7. 보고서 형식으로 사용자에게 제출
8. 사용자 승인 후 실행, 결과를 nst_tasks.result에 기록
9. 상태 전이: waiting_approval → completed/revising

## 보고서 형식

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 태스크 검토 완료: [task.id] [task.title]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

👥 참여 팀:
- 주담당: @[팀명] — [핵심 분석 1줄]
- 리뷰: @[팀명] — [피드백 1줄]

📊 종합 판단:
[팀 간 합의된 결론 2~3줄]

⚠️ 이견/리스크 (있을 경우):
- [팀A]: ~를 권고 / [팀B]: ~를 권고

✅ 실행 계획 (승인 시):
1. [구체적 실행 항목]

👉 승인하시면 실행합니다.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Supabase 프로젝트: `dtmoylnyzkbfjohnfkgd`, 테이블: `nst_tasks`, `nst_activity_log`
