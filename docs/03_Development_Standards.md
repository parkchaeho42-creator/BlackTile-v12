# BlackTile V12 - Development Standards (FINAL SPEC)

**Document ID:** 03  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 모든 코드 작성 규칙을 정의한다.

모든 Cell, Engine, Model, Test는 본 규칙을 반드시 준수해야 한다.

---

# 2. Core Coding Philosophy

- Code is execution of architecture
- No logic without specification
- No structure without documentation
- Simplicity > Complexity
- Stability > Speed
- Safety > Profit

---

# 3. File Rule

- 1 Cell = 1 Python file
- File name = snake_case
- No mixed responsibility files

예:

```
order_executor.py
risk_validator.py
signal_builder.py
```

---

# 4. Class Rule

- 1 Cell = 1 Main Class
- Class name = PascalCase
- No multiple core classes per file

예:

```python
class OrderExecutor:
    pass
```

---

# 5. Function Rule

- snake_case only
- Single responsibility
- No hidden side effects

예:

```python
def calculate_position_size():
    pass
```

---

# 6. Variable Rule

- snake_case only
- No abbreviations unless standard

예:

```
entry_price
stop_loss_price
position_size
```

---

# 7. Constant Rule

- UPPER_CASE
- Must be declared in config or constants module

예:

```
MAX_LEVERAGE = 10
RISK_LIMIT = 0.02
```

---

# 8. Type Safety Rule

- All functions MUST use type hints
- All models MUST be dataclasses or enums
- Dict usage is forbidden for core flow

예:

```python
def process_signal(signal: Signal) -> RiskReport:
    pass
```

---

# 9. Logging Rule

- print() 금지 (디버깅 제외)
- 반드시 Logger 사용
- 모든 중요한 이벤트 기록

로그 필수 항목:

- Signal 생성
- Risk 승인/거절
- Order 실행
- Error 발생
- System state change

---

# 10. Exception Rule

- 모든 external call은 try/except 필수
- 예외는 반드시 logging
- silent fail 금지

예:

```python
try:
    execute_order()
except Exception as e:
    logger.error(e)
    raise
```

---

# 11. Config Rule

다음은 절대 코드에 직접 작성 금지:

- API Key
- Secret Key
- Symbol
- Leverage
- Risk parameters
- AI parameters

→ 반드시 Config Layer 사용

---

# 12. AI Rule

AI는 절대 실행 주체가 아니다.

## Allowed

- Market analysis
- Pattern detection
- Risk scoring suggestion
- Parameter optimization

## Forbidden

- Order execution
- Risk override
- Decision override
- Position modification

---

# 13. Data Rule

- ALL communication MUST use Common Data Models
- Dict passing 금지
- Raw JSON 금지 (internal flow)

---

# 14. Testing Rule

모든 Cell은 테스트 가능해야 한다.

필수 테스트:

- Unit Test
- Integration Test
- E2E Test (필요 시)

---

# 15. Dependency Rule

- 하위 → 상위 호출 금지
- 순환 참조 금지
- Engine은 orchestration only

---

# 16. Error Handling Rule

- 모든 error는 logging 필수
- 시스템 중단 가능 error는 명시
- silent ignore 절대 금지

---

# 17. Code Review Rule

모든 코드 merge 전에:

- Spec 일치 여부 확인
- Test 통과 확인
- Logger 적용 확인
- Config 적용 확인
- Type hint 확인
- Dependency rule 확인

---

# 18. Definition of Done

Cell이 완료되기 위한 조건:

- 구현 완료
- 테스트 통과
- 로그 적용
- Config 분리
- 문서 일치
- 리뷰 통과

---

# 19. Golden Rule

> “If it is not in the spec, it does not exist.”
