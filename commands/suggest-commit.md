---
description: 현재 작업 내역을 분석하여 커밋 메시지와 브랜치명을 추천합니다.
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -5`

## Your task

위의 변경사항을 분석하여 다음을 추천해주세요:

### 1. 커밋 메시지 (한 줄)
- Conventional Commits 형식 사용: `<type>(<scope>): <description>`
- type: feat, fix, refactor, docs, test, chore, style, perf 중 선택
- scope: 변경된 모듈/컴포넌트 (선택사항)
- description: 변경 내용을 간결하게 영어로 작성

### 2. 브랜치명
- 형식: `<type>/<short-description>`
- 케밥 케이스 사용 (예: feature/add-user-auth)
- 간결하고 명확하게

### 출력 형식

```
📝 추천 커밋 메시지:
<커밋 메시지>

🌿 추천 브랜치명:
<브랜치명>
```

변경사항이 없으면 "변경사항이 없습니다"라고 알려주세요.
