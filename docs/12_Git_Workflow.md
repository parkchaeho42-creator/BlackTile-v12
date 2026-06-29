# BlackTile V12 - Git Workflow (FINAL SPEC)

**Document ID:** 12  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 Git 작업 흐름을 정의한다.

모든 변경은 반드시 본 규칙을 따른다.

---

# 2. BRANCH STRUCTURE

```
main        → production (LIVE)
develop     → integration
feature/*   → development
hotfix/*    → emergency fix
```

---

# 3. WORKFLOW RULE

## Step 1: Feature Development

```
feature/cell-xx-name
```

---

## Step 2: Development Merge

```
feature → develop
```

---

## Step 3: Test Gate

- Unit Test
- Integration Test
- E2E Test

---

## Step 4: Production Merge

```
develop → main
```

---

# 4. COMMIT RULE

## Format

```
[Cell-XX] type: description
```

## Types

- feat
- fix
- refactor
- test
- docs

---

# 5. CELL COMMIT RULE

예:

```
[Cell-42] feat: implement order executor
[Cell-38] fix: risk validation edge case
```

---

# 6. NO DIRECT MAIN PUSH

- main branch direct push 금지
- 모든 변경은 PR 필수

---

# 7. VERSION TAGGING

```
v12.0.0 → major system release
v12.0.1 → patch fix
```

---

# 8. ROLLBACK RULE

If failure detected:

```
git revert <commit>
or
git reset --hard <stable>
```

---

# 9. HOTFIX RULE

- Only for critical production issues
- Must be tested before merge

---

# 10. FINAL PRINCIPLE

> “No code is real until it passes Git flow.”
