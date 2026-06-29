# BlackTile V12 - Config Specification (FINAL SPEC)

**Document ID:** 06  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12 시스템의 모든 설정(Configuration) 구조를 정의한다.

모든 파라미터는 코드에 하드코딩 금지이며 반드시 Config를 통해 관리한다.

---

# 2. Config Philosophy

- Code ≠ Configuration
- No hardcoding allowed
- Environment-driven system
- Backtest / Paper / Live 분리 필수
- Single source of truth per parameter

---

# 3. CONFIG STRUCTURE

```
configs/
├── system.yaml
├── trading.yaml
├── risk.yaml
├── ai.yaml
├── exchange.yaml
├── logging.yaml
├── backtest.yaml
```

---

# 4. ENVIRONMENT MODES

시스템은 3가지 환경을 지원한다:

- BACKTEST
- PAPER
- LIVE

모든 설정은 환경별 override 가능해야 한다.

---

# 5. SYSTEM CONFIG (system.yaml)

```yaml
mode: BACKTEST  # BACKTEST | PAPER | LIVE

symbol: BTCUSDT
timeframe: 1m

timezone: UTC

debug: false
```

---

# 6. TRADING CONFIG (trading.yaml)

```yaml
max_position_size: 1.0
max_open_positions: 1

leverage:
  default: 5
  max: 10

entry:
  slippage_tolerance: 0.05
  order_type: MARKET
```

---

# 7. RISK CONFIG (risk.yaml)

```yaml
risk_per_trade: 0.01
max_drawdown: 0.15

stop_loss:
  atr_multiplier: 2.0

take_profit:
  rr_ratio: 2.0

leverage_cap: 10
```

---

# 8. AI CONFIG (ai.yaml)

```yaml
enabled: true

models:
  pattern_ai: true
  sentiment_ai: true
  risk_ai: true

weights:
  pattern: 0.4
  sentiment: 0.3
  risk: 0.3

threshold:
  confidence_min: 0.6
```

---

# 9. EXCHANGE CONFIG (exchange.yaml)

```yaml
exchange: binance

api:
  testnet: true
  recv_window: 5000

rate_limit:
  enabled: true
  max_requests_per_sec: 10
```

---

# 10. LOGGING CONFIG (logging.yaml)

```yaml
level: INFO

outputs:
  console: true
  file: true

paths:
  system: logs/system/
  trades: logs/trades/
  errors: logs/errors/
```

---

# 11. BACKTEST CONFIG (backtest.yaml)

```yaml
initial_balance: 10000

commission: 0.0004

slippage: 0.0005

data_source: historical

replay_speed: fast
```

---

# 12. CONFIG RULES

## Rule 1 - No Hardcoding

- API Key ❌
- Risk values ❌
- Strategy parameters ❌

→ 모두 Config에서만 관리

---

## Rule 2 - Environment Override

모든 config는 환경별 override 가능해야 한다.

예:

```
BACKTEST → aggressive risk allowed
LIVE → strict risk control
```

---

## Rule 3 - Immutable Runtime

런타임 중 config 변경 금지 (hot reload only via controlled system)

---

## Rule 4 - Central Access

모든 Cell은 반드시:

```
ConfigManager.get("risk.risk_per_trade")
```

형태로 접근해야 한다.

---

# 13. CONFIG MANAGER RULE

- Singleton 구조
- YAML 기반 로딩
- Environment 자동 감지
- Validation 필수

---

# 14. VALIDATION RULE

시스템 시작 시:

- 필수 키 존재 확인
- 타입 검증
- 범위 검증
- 누락 시 즉시 fail

---

# 15. SECURITY RULE

- API Key는 절대 코드 저장 금지
- .env 또는 secure vault 사용
- logs에 key 출력 금지

---

# 16. FINAL PRINCIPLE

> “Config defines behavior.  
> Code only executes behavior.”
