# BlackTile V12 - Deployment Guide (FINAL SPEC)

**Document ID:** 10  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12 시스템의 배포 및 운영 환경 구성을 정의한다.

모든 실행 환경은 동일한 코드 기반을 사용한다.

---

# 2. Deployment Philosophy

- Same code in all environments
- Only config changes between environments
- No logic modification in live system
- Fail-safe first
- Manual intervention minimized

---

# 3. DEPLOYMENT ENVIRONMENTS

```
Local (Dev)
   ↓
Colab (Test)
   ↓
VPS (Paper / Shadow)
   ↓
Mini PC (Live Trading)
```

---

# 4. SYSTEM REQUIREMENTS

## Minimum Specs

- CPU: 4 cores+
- RAM: 8GB+
- Storage: 50GB SSD
- Stable internet connection

---

# 5. INSTALLATION FLOW

## Step 1: Clone Repository

```bash
git clone https://github.com/your-repo/BlackTile-v12.git
cd BlackTile-v12
```

---

## Step 2: Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Step 3: Configure Environment

```bash
cp configs/system.yaml.example configs/system.yaml
```

Set mode:

- BACKTEST
- PAPER
- LIVE

---

## Step 4: Set API Keys

Store securely:

- Binance API Key
- Binance Secret Key

Never hardcode.

---

# 6. EXECUTION MODES

## BACKTEST

- Historical data only
- No API calls
- Replay engine enabled

---

## PAPER TRADING

- Real market data
- Simulated execution
- No real funds

---

## SHADOW LIVE

- Real signals
- No execution OR delayed execution logging
- Used for validation

---

## LIVE TRADING

- Real execution
- Real funds
- Full risk control active

---

# 7. BINANCE CONNECTION RULE

- USDT-M Futures only
- BTCUSDT only
- WebSocket + REST hybrid
- Rate limit handling required

---

# 8. SAFETY RULES

## Mandatory Safety Layers

- Risk Engine
- Decision Engine (Chairman)
- Protection Engine

No order can bypass these layers.

---

# 9. FAILURE RECOVERY

System must handle:

- API downtime
- Network delay
- WebSocket disconnect
- Order rejection
- Partial fills

Recovery strategy:

- Retry mechanism
- State sync
- Snapshot restore

---

# 10. STATE MANAGEMENT

- Position state stored in DB layer
- Snapshot every cycle
- Watchdog monitors inconsistency

---

# 11. LOGGING REQUIREMENTS

All environments must log:

- Signals
- Orders
- Decisions
- Errors
- System state changes

Logs must be persistent.

---

# 12. LIVE DEPLOYMENT RULE

Before LIVE activation:

- Backtest passed
- Paper trading stable
- E2E test passed
- No critical errors

---

# 13. MINI PC LIVE SETUP

Recommended:

- Ubuntu 22.04+
- Python 3.11+
- Auto-restart service (systemd)
- Remote SSH access

---

# 14. AUTO-START RULE

System must restart automatically on crash.

Example systemd service required.

---

# 15. MONITORING

Required monitoring:

- CPU usage
- Memory usage
- Trade success rate
- Drawdown
- API latency

---

# 16. ROLLBACK RULE

If live system fails:

- Switch to PAPER mode immediately
- Restore last stable snapshot
- Disable execution layer

---

# 17. SECURITY RULE

- API keys encrypted or env-based
- No key exposure in logs
- SSH access restricted

---

# 18. FINAL PRINCIPLE

> “Deployment is not launch.  
> Deployment is controlled survival in production.”
