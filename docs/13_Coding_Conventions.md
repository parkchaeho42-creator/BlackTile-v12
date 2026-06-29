# BlackTile V12 - Coding Conventions (FINAL SPEC)

**Document ID:** 13  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

코드 스타일과 구조 일관성을 정의한다.

---

# 2. NAMING RULES

## Files
- snake_case.py

## Classes
- PascalCase

## Functions
- snake_case

## Variables
- snake_case

---

# 3. INDENT RULE

- 4 spaces only
- tabs 금지

---

# 4. IMPORT RULE

```
standard → third-party → local
```

---

# 5. FILE STRUCTURE

```
imports
constants
dataclasses
class
functions
```

---

# 6. FUNCTION RULE

- 1 function = 1 responsibility
- max complexity low
- no hidden side effects

---

# 7. CLASS RULE

- single responsibility
- no god class
- no mixed domain logic

---

# 8. COMMENT RULE

- why only (not what)
- no redundant comments

---

# 9. ERROR RULE

- always explicit
- never silent fail

---

# 10. LOG RULE

- structured logging only
- no print()

---

# 11. TYPE HINT RULE

- mandatory for all functions

---

# 12. FINAL PRINCIPLE

> “Readable code is maintainable system.”
