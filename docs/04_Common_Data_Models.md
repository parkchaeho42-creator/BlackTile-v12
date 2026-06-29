# BlackTile V12 - Common Data Models (FINAL SPEC)

**Document ID:** 04  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12의 모든 Cell이 공통으로 사용하는 데이터 구조를 정의한다.

모든 데이터는 본 모델을 통해서만 전달된다.

dict / raw JSON 전달은 금지된다.

---

# 2. Design Philosophy

- Strongly Typed Data Flow
- Dataclass 기반 구조
- Immutable 중심 설계
- No ad-hoc structures
- Explicit contracts between Cells

---

# 3. Core Data Flow

```
MarketData → IndicatorSet → Signal → RiskReport → Decision → Order → ExecutionResult → Position
```

---

# 4. Base Rules

- 모든 모델은 dataclass 사용
- 모든 timestamp는 UTC
- 모든 금액은 float (V12 simplified)
- Enum 적극 사용
- Optional 최소화

---

# 5. ENUM DEFINITIONS

## Side

```python
class Side(Enum):
    LONG = "LONG"
    SHORT = "SHORT"
```

---

## OrderType

```python
class OrderType(Enum):
    MARKET = "MARKET"
    LIMIT = "LIMIT"
```

---

## SignalStrength

```python
class SignalStrength(Enum):
    LOW = "LOW"
    MEDIUM = "MEDIUM"
    HIGH = "HIGH"
```

---

# 6. CORE MODELS

---

## 6.1 MarketData

```python
@dataclass
class MarketData:
    symbol: str
    timestamp: datetime

    last_price: float
    bid_price: float
    ask_price: float

    volume: float
```

---

## 6.2 Candle

```python
@dataclass
class Candle:
    open_time: datetime
    close_time: datetime

    open: float
    high: float
    low: float
    close: float
    volume: float
```

---

## 6.3 OrderBook

```python
@dataclass
class OrderBook:
    best_bid: float
    best_ask: float

    bid_depth: float
    ask_depth: float

    spread: float
```

---

## 6.4 Trade

```python
@dataclass
class Trade:
    price: float
    quantity: float
    side: Side
    timestamp: datetime
```

---

## 6.5 IndicatorSet

```python
@dataclass
class IndicatorSet:
    ema: float
    rsi: float
    atr: float
    adx: float
    volume: float
    volatility: float
    market_regime: str
```

---

## 6.6 Signal

```python
@dataclass
class Signal:
    strategy_name: str
    side: Side

    entry_price: float
    confidence: float

    strength: SignalStrength
    timestamp: datetime
```

---

## 6.7 RiskReport

```python
@dataclass
class RiskReport:
    position_size: float
    stop_loss: float
    take_profit: float
    leverage: float

    expected_loss: float
    expected_reward: float
    risk_score: float
```

---

## 6.8 Decision

```python
@dataclass
class Decision:
    approved: bool
    confidence: float
    reject_reason: str
    timestamp: datetime
```

---

## 6.9 Order

```python
@dataclass
class Order:
    symbol: str
    side: Side
    order_type: OrderType

    quantity: float
    price: float

    reduce_only: bool
    time_in_force: str
```

---

## 6.10 ExecutionResult

```python
@dataclass
class ExecutionResult:
    order_id: str
    status: str

    filled_qty: float
    avg_price: float
    fee: float

    timestamp: datetime
```

---

## 6.11 Position

```python
@dataclass
class Position:
    side: Side
    quantity: float

    entry_price: float
    mark_price: float

    unrealized_pnl: float
    leverage: float
```

---

## 6.12 Account

```python
@dataclass
class Account:
    wallet_balance: float
    available_balance: float

    margin_ratio: float
    total_pnl: float
```

---

## 6.13 Performance

```python
@dataclass
class Performance:
    total_return: float
    win_rate: float
    profit_factor: float

    sharpe_ratio: float
    max_drawdown: float
    total_trades: int
```

---

# 7. Ownership Rules

| Model | Owner Cell |
|------|------------|
| MarketData | Data Pipeline |
| IndicatorSet | Indicator Engine |
| Signal | Strategy Engine |
| RiskReport | Risk Engine |
| Decision | Decision Engine |
| Order | Execution Engine |
| ExecutionResult | Execution Engine |
| Position | Position Manager |
| Performance | Analytics |

---

# 8. Data Contract Rule

- 모든 Cell은 반드시 이 모델만 사용
- dict 전달 금지
- JSON 직접 전달 금지
- 모델 변경 시 문서 먼저 수정

---

# 9. Immutability Rule

다음 모델은 변경 불가 개념으로 사용:

- Signal
- Decision
- Order
- ExecutionResult

---

# 10. Extension Policy

추가 모델은 반드시 이 문서에 등록 후 사용:

예:

- FundingRate (V13 예정)
- OpenInterest (V13 예정)
- Liquidation (V13 예정)
