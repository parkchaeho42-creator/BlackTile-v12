# BlackTile V12 - Development Standards

**Document ID:** 03  
**Version:** V12.0  
**Status:** Official  
**Last Updated:** 2026-06-29

---

# 1. Purpose

본 문서는 BlackTile V12 프로젝트의 공식 개발 규약을 정의한다.

모든 소스코드, Cell, 테스트 및 문서는 본 규약을 준수해야 한다.

---

# 2. Core Principles

## Rule 1. Documentation First

모든 기능은 구현 전에 문서가 먼저 작성되어야 한다.

---

## Rule 2. One Cell = One Responsibility

하나의 Cell은 하나의 책임만 가진다.

---

## Rule 3. One Cell = One Python File

하나의 Cell은 하나의 Python 파일로 구현한다.

---

## Rule 4. One Cell = One Main Class

각 Cell은 하나의 핵심 Class만 가진다.

---

## Rule 5. Single Source of Truth

동일한 정보는 하나의 위치에서만 관리한다.

---

## Rule 6. Configuration Driven

설정값은 코드에 하드코딩하지 않고 Config에서 관리한다.

---

## Rule 7. Fail Safe

오류 발생 시 시스템은 안전한 상태로 전환되어야 한다.

---

## Rule 8. Testable Design

모든 Cell은 독립적으로 테스트 가능해야 한다.

---

# 3. Dependency Rules

- 순환 참조를 금지한다.
- 하위 계층은 상위 계층을 참조하지 않는다.
- Engine은 각 계층을 연결만 한다.

---

# 4. Coding Rules

- Python 3.11 이상 사용
- PEP 8 준수
- Type Hint 필수
- Dataclass 적극 사용
- Enum 적극 사용
- Magic Number 금지
- 하드코딩 금지

---

# 5. Naming Rules

## File

snake_case.py

예)

```
order_builder.py
market_regime.py
```

---

## Class

PascalCase

예)

```
OrderBuilder
RiskValidator
```

---

## Function

snake_case

예)

```
calculate_risk()
build_signal()
```

---

## Variable

snake_case

예)

```
entry_price
position_size
```

---

## Constant

UPPER_CASE

예)

```
MAX_LEVERAGE
DEFAULT_TIMEOUT
```

---

# 6. Logging Rules

- print()는 디버깅 목적 외 사용하지 않는다.
- Logger를 사용한다.
- 모든 예외를 기록한다.
- 주요 이벤트를 기록한다.

---

# 7. Exception Rules

외부 API 호출은 반드시 예외 처리를 수행한다.

예외를 무시하거나 `pass`로 처리하지 않는다.

---

# 8. Configuration Rules

다음 정보는 Config에서만 관리한다.

- API Key
- Secret
- Symbol
- Leverage
- Risk
- Strategy Parameter
- Telegram
- AI Parameter

---

# 9. AI Rules

AI는 다음만 수행한다.

- 시장 분석
- 패턴 분석
- 위험 점수
- 파라미터 추천

AI는 다음을 수행하지 않는다.

- 주문 실행
- Position 변경
- Risk 우회
- Chairman 우회

---

# 10. Testing Rules

모든 Cell은 다음 테스트를 수행한다.

- Unit Test
- Integration Test
- 필요 시 E2E Test

---

# 11. Documentation Rules

모든 Cell은 다음 내용을 문서화한다.

- 목적
- 입력
- 출력
- 의존성
- 예외 처리
- 테스트 방법

---

# 12. Code Review Checklist

코드를 병합하기 전에 다음 항목을 확인한다.

- 기능 구현 완료
- 테스트 통과
- Logger 적용
- Config 사용
- Type Hint 적용
- 예외 처리 완료
- 문서 업데이트 완료

---

# 13. Definition of Done

하나의 Cell은 아래 조건을 모두 만족해야 완료로 간주한다.

- 구현 완료
- 테스트 통과
- 문서 작성 완료
- Logger 적용
- Config 적용
- 코드 리뷰 완료
