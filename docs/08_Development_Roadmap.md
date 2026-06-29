# BlackTile V12 - Development Roadmap (FINAL SPEC)

**Document ID:** 08  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 개발 순서와 단계별 구현 전략을 정의한다.

모든 개발은 반드시 본 로드맵 순서를 따른다.

---

# 2. Development Philosophy

- Bottom-up implementation
- Core first, extension later
- Backtest before live
- Stability before optimization
- No skipping layers

---

# 3. DEVELOPMENT PHASES

전체 개발은 5단계로 구성된다.

```
Phase 0 → Bootstrap
Phase 1 → Data + Indicator Core
Phase 2 → Strategy + Risk Core
Phase 3 → Decision + Execution Core
Phase 4 → Protection + Analytics
Phase 5 → AI + Optimization + Live
```

---

# 4. PHASE 0 - BOOTSTRAP (Cell 01–08)

## 목표

시스템 기반 구축

## Cell

- 01 Project Bootstrap
- 02 Environment
- 03 Config Loader
- 04 Secrets Manager
- 05 Logger
- 06 Diagnostics
- 07 Clock
- 08 State Manager

## 완료 기준

- 시스템 실행 가능
- Config 로딩 성공
- Logger 정상 작동

---

# 5. PHASE 1 - DATA + INDICATORS (Cell 09–23)

## 목표

시장 데이터 수집 및 분석 기반 구축

## Cell

### Data Pipeline
- 09 WebSocket Input
- 10 REST Collector
- 11 Normalizer
- 12 OrderBook
- 13 Trade Flow
- 14 Cache
- 15 WAL Logger
- 16 Replay Engine

### Indicators
- 17 EMA
- 18 RSI
- 19 ATR
- 20 ADX
- 21 Volume
- 22 Volatility
- 23 Market Regime

## 완료 기준

- 실시간 데이터 수집
- Indicator 정상 계산
- Replay 가능

---

# 6. PHASE 2 - STRATEGY + RISK (Cell 24–38)

## 목표

매매 판단 구조 생성

## Cell

### Strategy
- 24 Trend Scouter
- 25 Sweep Detector
- 26 Reclaim Detector
- 27 Breakout Detector
- 28 Pullback Detector
- 29 Signal Filter
- 30 Strategy Selector
- 31 Signal Builder

### Risk
- 32 Position Sizer
- 33 Leverage Manager
- 34 StopLoss Calculator
- 35 TakeProfit Calculator
- 36 Drawdown Guard
- 37 Portfolio Guard
- 38 Risk Validator

## 완료 기준

- Signal 생성 가능
- Risk 승인 구조 작동

---

# 7. PHASE 3 - DECISION + EXECUTION (Cell 39–46)

## 목표

최종 거래 실행 구조

## Cell

### Decision
- 39 Confidence Score
- 40 Chairman

### Execution
- 41 Order Builder
- 42 Order Executor
- 43 Order Monitor
- 44 SL/TP Manager
- 45 Trailing Manager
- 46 Position Manager

## 완료 기준

- 승인 기반 주문 실행
- Position 정상 관리

---

# 8. PHASE 4 - PROTECTION + ANALYTICS (Cell 47–58)

## 목표

안정성 + 기록 시스템

## Cell

### Protection
- 47 Iron Gate
- 48 Circuit Breaker
- 49 State Sync
- 50 Snapshot
- 51 Watchdog

### Analytics
- 52 Signal Logger
- 53 Trade Logger
- 54 Decision Logger
- 55 Error Logger
- 56 Performance Analyzer
- 57 Report Generator
- 58 Telegram Bot

## 완료 기준

- 장애 감지 가능
- 모든 거래 기록 저장

---

# 9. PHASE 5 - AI + FINAL SYSTEM (Cell 59–66)

## 목표

AI 보조 + 시스템 완성

## Cell

- 59 News Sentiment AI
- 60 Pattern AI
- 61 Market Regime AI
- 62 Risk AI
- 63 Parameter Optimizer
- 64 Trade Reviewer
- 65 Learning Manager
- 66 BlackTile Engine

## 완료 기준

- AI 분석 결과 반영
- Engine orchestration 완성

---

# 10. TEST PHASE (Cell 67–69)

## 목표

전체 시스템 검증

## Cell

- 67 Unit Test
- 68 Integration Test
- 69 E2E Test

---

# 11. DEPLOYMENT FLOW

순서:

```
Backtest
  ↓
Paper Trading
  ↓
Shadow Live
  ↓
Live Trading
```

---

# 12. SUCCESS CRITERIA

- Backtest = Paper 결과 일치
- Paper = Live 구조 동일
- No crash in 24h run
- Drawdown controlled
- Execution latency stable

---

# 13. REAL-WORLD CONSTRAINTS

- Binance BTCUSDT only
- 1 symbol only
- 1 strategy set initially
- No multi-exchange

---

# 14. FINAL PRINCIPLE

> “Do not optimize before it works.  
> Do not scale before it is stable.”
