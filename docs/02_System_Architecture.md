# BlackTile V12 - System Architecture (FINAL SPEC)

**Document ID:** 02  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 전체 시스템 구조와 Cell 기반 아키텍처를 정의한다.

모든 구현은 본 구조를 절대적으로 따른다.

---

# 2. Architecture Overview

BlackTile V12는 **Cell-based Layered Architecture**이다.

각 Layer는 독립적인 책임을 가지며, 단방향으로만 흐른다.

---

# 3. Full System Flow

```
[Bootstrap]
      ↓
[Data Pipeline]
      ↓
[Indicator Engine]
      ↓
[Strategy Engine]
      ↓
[Risk Engine]
      ↓
[Decision Engine]
      ↓
[Execution Engine]
      ↓
[Protection Engine]
      ↓
[Database & Analytics]
      ↓
[AI Engine]
      ↓
[BlackTile Engine]
```

---

# 4. Cell System Structure (84 Cells)

## 📦 A. Bootstrap (Cell 01–08)

- Cell 01: Project Bootstrap
- Cell 02: Environment Detection
- Cell 03: Config Loader
- Cell 04: Secrets Manager
- Cell 05: Logger System
- Cell 06: Diagnostics System
- Cell 07: Clock Abstraction
- Cell 08: State Manager

---

## 📡 B. Data Pipeline (Cell 09–16)

- Cell 09: WebSocket Input
- Cell 10: REST Collector
- Cell 11: Data Normalizer
- Cell 12: OrderBook Processor
- Cell 13: Trade Flow Analyzer
- Cell 14: Candle Cache
- Cell 15: WAL Logger
- Cell 16: Replay Engine

---

## 📈 C. Indicator Engine (Cell 17–23)

- Cell 17: EMA Analyzer
- Cell 18: RSI Analyzer
- Cell 19: ATR Analyzer
- Cell 20: ADX Analyzer
- Cell 21: Volume Analyzer
- Cell 22: Volatility Analyzer
- Cell 23: Market Regime Detector

---

## 🎯 D. Strategy Engine (Cell 24–31)

- Cell 24: Trend Scouter
- Cell 25: Sweep Detector
- Cell 26: Reclaim Detector
- Cell 27: Breakout Detector
- Cell 28: Pullback Detector
- Cell 29: Signal Filter
- Cell 30: Strategy Selector
- Cell 31: Signal Builder

---

## ⚖️ E. Risk Engine (Cell 32–38)

- Cell 32: Position Sizer
- Cell 33: Leverage Manager
- Cell 34: StopLoss Calculator
- Cell 35: TakeProfit Calculator
- Cell 36: Drawdown Guard
- Cell 37: Portfolio Guard
- Cell 38: Risk Validator

---

## 👑 F. Decision Engine (Cell 39–40)

- Cell 39: Confidence Score Engine
- Cell 40: Chairman (Final Approval)

---

## 🚀 G. Execution Engine (Cell 41–46)

- Cell 41: Order Builder
- Cell 42: Order Executor
- Cell 43: Order Monitor
- Cell 44: SL/TP Manager
- Cell 45: Trailing Stop Manager
- Cell 46: Position Manager

---

## 🛡️ H. Protection Engine (Cell 47–51)

- Cell 47: Iron Gate
- Cell 48: Circuit Breaker
- Cell 49: State Sync
- Cell 50: Snapshot Manager
- Cell 51: Watchdog

---

## 📒 I. Database & Analytics (Cell 52–58)

- Cell 52: Signal Logger
- Cell 53: Trade Logger
- Cell 54: Decision Logger
- Cell 55: Error Logger
- Cell 56: Performance Analyzer
- Cell 57: Report Generator
- Cell 58: Telegram Bot

---

## 🤖 J. AI Engine (Cell 59–65)

- Cell 59: News Sentiment AI
- Cell 60: Pattern AI
- Cell 61: Market Regime AI
- Cell 62: Risk AI
- Cell 63: Parameter Optimizer
- Cell 64: Trade Reviewer
- Cell 65: Learning Manager

---

## ⚙️ K. Engine (Cell 66)

- Cell 66: BlackTile Engine (Orchestrator Only)

---

## 🧪 L. Test Layer (Cell 67–69)

- Cell 67: Unit Test
- Cell 68: Integration Test
- Cell 69: E2E Test

---

# 5. Dependency Rules

## Allowed Direction

```
Bootstrap → Data → Indicator → Strategy → Risk → Decision → Execution → Protection → DB → AI → Engine
```

## Forbidden

- Reverse dependency ❌
- Cross-layer direct calls ❌
- Circular dependency ❌

---

# 6. Engine Rule (Critical)

Cell 66 (BlackTile Engine) MUST NOT:

- Make trading decisions
- Calculate signals
- Modify risk
- Execute logic

It ONLY orchestrates flow.

---

# 7. Data Contract Rule

All Cells MUST use:

- Common Data Models (strict)
- No raw dict passing
- No ad-hoc structures

---

# 8. Execution Safety Rule

No order can be executed unless:

- Signal exists
- Risk approved
- Decision approved
- System state is healthy

---

# 9. Runtime Modes

Same architecture supports:

- Backtest
- Paper Trading
- Shadow Live
- Live Trading

Only adapters change, NOT logic.

---

# 10. AI Placement Rule

AI is ONLY allowed in:

- Analysis
- Scoring
- Recommendation

AI is NEVER allowed in:

- Execution
- Risk override
- Decision override

---

# 11. Expansion Rule

V12 is frozen:

- No multi-symbol expansion
- No multi-exchange support
- No architecture change without version upgrade

---

# 12. Final Principle

> Architecture is law.  
> Code must obey architecture, not the opposite.
