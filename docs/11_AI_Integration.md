# BlackTile V12 - AI Integration (FINAL SPEC)

**Document ID:** 11  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Purpose

본 문서는 BlackTile V12에서 AI의 역할과 제한 범위를 정의한다.

AI는 의사결정자가 아니라 **분석 보조 시스템**이다.

---

# 2. AI Philosophy

- AI ≠ Decision Maker
- AI = Advisor only
- AI = Probability enhancer
- AI = Risk assistant
- AI cannot execute trades

---

# 3. AI POSITION IN SYSTEM

```
Strategy → Risk → Decision → Execution
                 ↑
                AI (Support Layer)
```

AI는 메인 플로우를 변경할 수 없다.

---

# 4. AI MODULES

## 1. Pattern AI (Cell 60)

- 시장 패턴 분석
- 구조 인식
- 반복 패턴 탐지

Output:
- pattern_score
- pattern_type

---

## 2. Sentiment AI (Cell 59)

- 뉴스 분석
- 시장 감정 평가

Output:
- sentiment_score
- bias_direction

---

## 3. Market Regime AI (Cell 61)

- 시장 상태 판단
  - trending
  - ranging
  - volatile

Output:
- regime_type
- confidence

---

## 4. Risk AI (Cell 62)

- 리스크 보조 평가
- 변동성 기반 위험 점수

Output:
- risk_score
- volatility_forecast

---

## 5. Parameter Optimizer (Cell 63)

- 전략 파라미터 추천
- 백테스트 기반 튜닝

Output:
- optimized_parameters

---

## 6. Trade Reviewer (Cell 64)

- 과거 거래 평가
- 전략 개선 피드백

Output:
- performance_feedback

---

## 7. Learning Manager (Cell 65)

- 시스템 학습 기록 관리
- 패턴 저장

Output:
- learning_state

---

# 5. AI INPUT RULE

AI는 반드시 다음만 입력으로 받는다:

- MarketData
- IndicatorSet
- Signal
- RiskReport
- Historical Trade Data

---

# 6. AI OUTPUT RULE

AI 출력은 반드시:

- Recommendation only
- No execution command
- No direct order instructions

---

# 7. AI FORBIDDEN ACTIONS

AI는 다음을 절대 수행할 수 없다:

- Order execution
- Position modification
- Risk override
- Decision override
- Strategy replacement

---

# 8. AI vs DECISION ENGINE

| Component | Role |
|----------|------|
| AI Engine | Suggestion |
| Chairman (Decision Engine) | Final decision |

---

# 9. AI CONFIDENCE RULE

AI output must include confidence score:

```
0.0 ~ 1.0
```

- Below 0.6 → ignored by Decision Engine
- Above 0.8 → high priority suggestion

---

# 10. AI OVERRIDE RULE

AI cannot override:

- Risk Engine
- Decision Engine
- Execution Engine

---

# 11. AI USAGE STRATEGY

AI is used only for:

- Filtering noise
- Enhancing probability
- Risk awareness
- Strategy tuning

---

# 12. SYSTEM FLOW WITH AI

```
Market Data
    ↓
Indicators
    ↓
Strategy
    ↓
AI Analysis (parallel)
    ↓
Risk Engine
    ↓
Decision Engine
    ↓
Execution
```

---

# 13. AI FAIL-SAFE RULE

If AI fails:

- System continues without AI
- No blocking allowed
- No dependency on AI for execution

---

# 14. MODEL INDEPENDENCE RULE

AI models must be:

- Replaceable
- Independent
- Non-critical to execution

---

# 15. FINAL PRINCIPLE

> “AI informs.  
> System decides.  
> Engine executes.”
