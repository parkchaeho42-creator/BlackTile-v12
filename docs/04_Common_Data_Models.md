# BlackTile V12 - Common Data Models

**Document ID:** 04  
**Version:** V12.0  
**Status:** Official  
**Last Updated:** 2026-06-29

---

# 1. Purpose

본 문서는 BlackTile V12에서 사용하는 공통 데이터 모델을 정의한다.

모든 Cell은 본 문서에 정의된 데이터 모델만 사용한다.

Dictionary(dict)를 이용한 임의 데이터 전달은 허용하지 않는다.

---

# 2. Design Principles

모든 데이터 모델은 다음 원칙을 따른다.

- Python Dataclass 사용
- Type Hint 필수
- UTC 시간 사용
- Immutable 객체 우선
- Enum 적극 사용
- Nullable 최소화

---

# 3. Data Flow

```
MarketData
      │
      ▼
IndicatorSet
      │
      ▼
Signal
      │
      ▼
RiskReport
      │
      ▼
Decision
      │
      ▼
Order
      │
      ▼
ExecutionResult
      │
      ▼
Position
      │
      ▼
Performance
```

---

# 4. Core Models

| Model | Producer | Consumer |
|--------|----------|----------|
| MarketData | Data Pipeline | Indicator Engine |
| Candle | Data Pipeline | Indicator Engine |
| OrderBook | Data Pipeline | Strategy Engine |
| Trade | Data Pipeline | Strategy Engine |
| IndicatorSet | Indicator Engine | Strategy Engine |
| Signal | Strategy Engine | Risk Engine |
| RiskReport | Risk Engine | Decision Engine |
| Decision | Decision Engine | Execution Engine |
| Order | Order Builder | Order Executor |
| ExecutionResult | Order Executor | Position Manager |
| Position | Position Manager | Database |
| Account | Exchange | Risk Engine |
| Performance | Database | Report |

---

# 5. Model Specifications

## MarketData

목적

실시간 시장 데이터 전달

필수 필드

- symbol
- timestamp
- last_price
- bid_price
- ask_price
- volume

생성

- WS Input
- REST Collector

사용

- Indicator Engine

---

## Candle

OHLCV 데이터

필드

- open
- high
- low
- close
- volume
- open_time
- close_time

---

## OrderBook

호가 데이터

필드

- best_bid
- best_ask
- bid_depth
- ask_depth
- spread

---

## Trade

체결 데이터

필드

- price
- quantity
- side
- timestamp

---

## IndicatorSet

기술지표 집합

포함

- EMA
- RSI
- ATR
- ADX
- Volume
- Volatility
- Market Regime

생성

Indicator Engine

---

## Signal

전략 신호

필드

- strategy_name
- side
- entry_price
- confidence
- timestamp

생성

Signal Builder

Immutable

YES

---

## RiskReport

리스크 평가 결과

필드

- position_size
- stop_loss
- take_profit
- leverage
- expected_loss
- expected_reward
- risk_score

생성

Risk Engine

---

## Decision

최종 승인

필드

- approved
- confidence
- reject_reason
- timestamp

생성

Chairman

---

## Order

거래소 주문

필드

- symbol
- side
- type
- quantity
- price
- reduce_only
- time_in_force

생성

Order Builder

---

## ExecutionResult

주문 결과

필드

- order_id
- status
- filled_qty
- avg_price
- fee
- timestamp

생성

Order Executor

---

## Position

현재 포지션

필드

- side
- quantity
- entry_price
- mark_price
- unrealized_pnl
- leverage

수정

Position Manager만 가능

---

## Account

계좌 상태

필드

- wallet_balance
- available_balance
- margin_ratio
- total_pnl

---

## Performance

성과 분석

필드

- total_return
- win_rate
- profit_factor
- sharpe_ratio
- max_drawdown
- total_trades

---

# 6. Rules

- 공통 모델 외 데이터 전달 금지
- Dict 전달 금지
- Model 변경 시 문서를 먼저 수정한다.
- 새로운 Model은 본 문서에 등록 후 구현한다.

---

# 7. Ownership

| Model | Owner |
|--------|-------|
| MarketData | Data Pipeline |
| IndicatorSet | Indicator Engine |
| Signal | Strategy Engine |
| RiskReport | Risk Engine |
| Decision | Decision Engine |
| Order | Execution Engine |
| Position | Position Manager |
| Performance | Analytics |

---

# 8. Future Extensions

향후 추가 가능 모델

- FundingRate
- OpenInterest
- Liquidation
- NewsEvent
- AIScore

V12에서는 구현 대상이 아니며, 구조적 확장만 고려한다.
