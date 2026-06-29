# BlackTile V12 - Project Structure (FINAL SPEC)

**Document ID:** 05  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 실제 코드 구조를 정의한다.

모든 코드 파일은 본 구조를 따라야 하며, 임의 구조 생성은 금지된다.

---

# 2. Root Project Structure

```
BlackTile-v12/
│
├── src/
├── configs/
├── tests/
├── scripts/
├── data/
├── logs/
├── notebooks/
├── docs/
├── README.md
└── requirements.txt
```

---

# 3. SRC (Core System)

```
src/
│
├── bootstrap/
├── data_pipeline/
├── indicators/
├── strategy/
├── risk/
├── decision/
├── execution/
├── protection/
├── database/
├── ai/
├── engine/
├── shared/
└── interfaces/
```

---

# 4. CELL MAPPING RULE

각 Cell은 반드시 1개의 Python file로 존재한다.

예:

```
Cell 41 → src/execution/order_builder.py
Cell 42 → src/execution/order_executor.py
Cell 40 → src/decision/chairman.py
```

---

# 5. LAYER DIRECTORY RULE

## Bootstrap
```
src/bootstrap/
```
- system init
- environment
- config loader
- logger
- state manager

---

## Data Pipeline
```
src/data_pipeline/
```
- websocket
- rest collector
- normalization
- orderbook
- trade flow
- cache
- replay

---

## Indicators
```
src/indicators/
```
- EMA
- RSI
- ATR
- ADX
- volume
- volatility
- regime

---

## Strategy
```
src/strategy/
```
- signal generation
- pattern detection
- filtering
- strategy selection

---

## Risk
```
src/risk/
```
- position sizing
- leverage control
- stop loss
- take profit
- validation

---

## Decision
```
src/decision/
```
- confidence scoring
- chairman approval

---

## Execution
```
src/execution/
```
- order building
- order execution
- monitoring
- position management

---

## Protection
```
src/protection/
```
- circuit breaker
- watchdog
- snapshot
- system safety

---

## Database
```
src/database/
```
- logging
- analytics
- reporting

---

## AI
```
src/ai/
```
- sentiment
- pattern AI
- risk AI
- optimization

---

## Engine
```
src/engine/
```
- orchestration only
- NO BUSINESS LOGIC

---

## Shared
```
src/shared/
```
- data models
- enums
- exceptions
- utilities

---

## Interfaces
```
src/interfaces/
```
- exchange connectors
- Binance API wrapper

---

# 6. CONFIG STRUCTURE

```
configs/
├── system.yaml
├── trading.yaml
├── risk.yaml
├── ai.yaml
├── exchange.yaml
```

---

# 7. TEST STRUCTURE

```
tests/
├── unit/
├── integration/
├── e2e/
```

---

# 8. LOG STRUCTURE

```
logs/
├── system/
├── trades/
├── errors/
├── performance/
```

---

# 9. DATA STRUCTURE

```
data/
├── historical/
├── replay/
├── backtest/
```

---

# 10. IMPORT RULES

## Allowed

- lower → upper layer only
- shared can be used everywhere
- interfaces only used by pipeline/execution

## Forbidden

- strategy importing execution ❌
- risk importing decision ❌
- circular imports ❌

---

# 11. CELL ISOLATION RULE

Each Cell:

- must NOT know other cells internally
- communicates ONLY via shared models
- no direct function calls across layers

---

# 12. ENGINE RULE

```
engine/
```

- ONLY orchestration
- NO calculation
- NO decision making
- NO strategy logic

---

# 13. SCALABILITY RULE

New feature must follow:

1. Create new Cell OR
2. Extend existing layer module
3. NEVER modify unrelated layers

---

# 14. GOLDEN STRUCTURE RULE

> “Structure defines execution.  
> Code cannot violate structure.”
