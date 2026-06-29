# BlackTile V12 - Master Index (FINAL SPEC)

**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures Automated Trading System

---

# 1. System Overview

BlackTile V12는 Binance BTCUSDT 무기한 선물 전용 자동매매 시스템이다.

모든 전략, 데이터 처리, 리스크 관리, 실행 로직은 단일 엔진 구조에서 동작한다.

---

# 2. Core Philosophy

- One Cell = One Responsibility
- One Cell = One File
- One Engine = Orchestration Only
- AI = Advisory Only (No Execution)
- Single Source of Truth (Data Models)
- Configuration Driven System
- Backtest == Live Logic 동일 구조

---

# 3. Layered Architecture

```
Bootstrap
Data Pipeline
Indicator Engine
Strategy Engine
Risk Engine
Decision Engine
Execution Engine
Protection Engine
Database & Analytics
AI Engine
BlackTile Engine
```

---

# 4. Runtime Modes

모든 로직은 동일하며 실행 환경만 다르다.

- Backtest Mode
- Paper Trading Mode
- Shadow Live Mode
- Live Trading Mode

---

# 5. System Constraints

- Binance USDT-M Futures ONLY
- BTCUSDT Perpetual ONLY
- No multi-exchange support
- No multi-symbol support (V12 scope)
- No manual trading logic inside cells

---

# 6. Data Flow Standard

```
MarketData → IndicatorSet → Signal → RiskReport → Decision → Order → ExecutionResult → Position
```

---

# 7. Execution Rule

- Strategy does NOT execute orders
- Risk does NOT execute orders
- Decision Engine (Chairman) is final authority
- Execution Engine only executes approved orders

---

# 8. AI Rule

AI is strictly advisory:

Allowed:
- Pattern analysis
- Market regime detection
- Risk scoring suggestions
- Parameter optimization

Forbidden:
- Order execution
- Position modification
- Risk override

---

# 9. Cell System Rule

Each Cell must satisfy:

- Single Responsibility
- Fully testable
- Independent execution possible
- Strict input/output contract
- No cross-layer logic leakage

---

# 10. Engineering Principle

System must always prioritize:

1. Stability
2. Predictability
3. Risk control
4. Reproducibility
5. Maintainability
6. Profitability (last priority)

---

# 11. Version Philosophy

V12 is:

- Single exchange system
- Single symbol system
- High stability focused
- Production-first architecture

Future expansion (V13+) may include:
- Multi-symbol
- Multi-exchange
- Portfolio system
