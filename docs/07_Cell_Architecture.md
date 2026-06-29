# BlackTile V12 - Cell Architecture (FINAL SPEC)

**Document ID:** 07  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 모든 Cell 구조와 공통 설계 패턴을 정의한다.

모든 Cell은 본 문서의 Base Template을 반드시 따른다.

---

# 2. Cell Philosophy

- 1 Cell = 1 Responsibility
- 1 Cell = 1 File
- 1 Cell = 1 Main Class
- No hidden logic
- No cross-layer dependency
- Pure input/output structure

---

# 3. CELL LIFECYCLE

```
Input → Process → Output
```

모든 Cell은 위 구조만 가진다.

---

# 4. BASE CELL TEMPLATE

모든 Cell은 다음 구조를 따른다:

```python
class BaseCell:
    def __init__(self, config, logger):
        self.config = config
        self.logger = logger

    def validate(self):
        pass

    def process(self, input_data):
        pass

    def run(self, input_data):
        self.validate()
        result = self.process(input_data)
        return result
```

---

# 5. CELL INTERFACE RULE

모든 Cell은 반드시:

## INPUT

- Dataclass only
- No dict
- No raw JSON

## OUTPUT

- Dataclass only
- Strict schema

---

# 6. CELL TYPES

## 1. Producer Cell

데이터 생성

예:
- Data Pipeline
- Indicator Engine

---

## 2. Processor Cell

데이터 가공

예:
- Strategy Engine
- Risk Engine

---

## 3. Decision Cell

결정 수행

예:
- Chairman (Decision Engine)

---

## 4. Execution Cell

외부 실행

예:
- Order Executor

---

## 5. Protection Cell

시스템 보호

예:
- Circuit Breaker
- Watchdog

---

# 7. CELL STRUCTURE STANDARD

모든 Cell 파일 구조:

```
class XXXCell:
    __init__
    validate()
    process()
    run()
```

---

# 8. CELL COMMUNICATION RULE

Cell 간 통신:

```
Cell A → Dataclass → Cell B
```

직접 함수 호출 금지

---

# 9. DEPENDENCY RULE

허용:

- 하위 Layer → 상위 Layer 없음
- Shared Models만 공통 사용
- Engine은 orchestration만 수행

금지:

- Cross-layer import
- Circular dependency
- Direct execution bypass

---

# 10. STATE RULE

- Cell은 상태를 직접 저장하지 않는다
- 상태는 State Manager 또는 Database Cell이 담당

---

# 11. ERROR HANDLING RULE

모든 Cell은 반드시:

```python
try:
    ...
except Exception as e:
    logger.error(e)
    raise
```

silent fail 금지

---

# 12. LOGGING RULE

모든 Cell은 최소 로그 포함:

- start
- success
- failure
- critical events

---

# 13. VALIDATION RULE

모든 Cell 입력은:

- type check
- null check
- range check

---

# 14. PERFORMANCE RULE

- heavy computation은 Indicator / Strategy로 분리
- Execution Cell은 lightweight 유지
- blocking logic 금지

---

# 15. CELL ISOLATION RULE

각 Cell은 독립적으로 실행 가능해야 한다.

---

# 16. ENGINE INTERACTION RULE

Engine은 Cell을 직접 “결정”하지 않는다.

Engine 역할:

- 순서 실행
- 데이터 전달
- 상태 관리

---

# 17. AI CELL RULE

AI Cell은:

- input 분석
- score 제공

금지:

- execution
- decision override

---

# 18. FINAL CELL PRINCIPLE

> “A Cell is not a module.  
> A Cell is a controlled execution unit.”
