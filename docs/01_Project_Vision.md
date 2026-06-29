# BlackTile V12 - Project Vision (FINAL SPEC)

**Document ID:** 01  
**Version:** V12.0  
**Status:** Final Specification  
**Scope:** Binance BTCUSDT Perpetual Futures System

---

# 1. Project Vision

BlackTile V12는 단순 자동매매 프로그램이 아니라  
**“구조화된 트레이딩 실행 시스템”**이다.

모든 의사결정은 감정이 아닌 **데이터 + 규칙 + 구조**로 결정된다.

---

# 2. Core Objective

본 프로젝트의 목표는 다음 3가지이다:

## 1) 안정성
- 24시간 무중단 실행
- 장애 발생 시 자동 복구
- 손실 제한 구조 필수

## 2) 재현성
- Backtest = Live 동일 로직
- 동일 입력 → 동일 출력 보장
- 모든 결정 로그 기록

## 3) 통제된 자동화
- AI는 보조 역할
- 최종 결정은 시스템 규칙 기반
- 인간 개입 최소화

---

# 3. Trading Philosophy

BlackTile V12는 다음 철학을 따른다:

## 1. 시장은 확률 구조다
- 100% 예측 불가
- 따라서 “승률 + 손익비 + 리스크”로 접근

## 2. 한 번의 거래보다 생존이 중요
- 계좌 생존 우선
- Drawdown 제어 필수

## 3. 과최적화 금지
- 단기 성과보다 구조 안정성 우선
- 전략은 단순할수록 좋다

---

# 4. System Boundaries

## In Scope

- BTCUSDT Perpetual Futures
- Binance USDT-M Only
- Fully automated execution system
- Risk-managed trading
- AI-assisted analysis

## Out of Scope

- 현물 거래
- 알트코인 확장
- 다중 거래소
- 수동 트레이딩
- 고빈도 초저지연 HFT

---

# 5. Automation Level

BlackTile V12 자동화 수준:

| 영역 | 자동화 수준 |
|------|------------|
| 데이터 수집 | Full Auto |
| 전략 생성 | Semi Auto |
| 리스크 판단 | Rule-based Auto |
| 주문 실행 | Full Auto |
| 최종 승인 | System Controlled |
| AI 판단 | Advisory Only |

---

# 6. Decision Hierarchy

모든 거래는 아래 순서를 따른다:

```
Market Data
    ↓
Indicator Engine
    ↓
Strategy Engine
    ↓
Risk Engine
    ↓
Decision Engine (Chairman)
    ↓
Execution Engine
    ↓
Protection Engine
```

---

# 7. Key Principle

## “No Blind Trading”

어떤 주문도 아래 조건 없이 실행되지 않는다:

- Signal 존재
- Risk 승인
- Decision 승인
- System 상태 정상

---

# 8. Risk Philosophy

리스크는 수익보다 우선이다.

- 손실 제한이 없는 전략은 금지
- 레버리지는 시스템이 결정
- 포지션 사이즈는 자동 계산

---

# 9. AI Philosophy

AI는 절대 “결정자”가 아니다.

AI 역할:
- 패턴 분석
- 시장 상태 평가
- 리스크 보조 점수
- 파라미터 추천

AI 금지:
- 주문 실행
- 포지션 변경
- 전략 override

---

# 10. Execution Philosophy

Execution Engine은 단순 실행기이다.

- 판단 금지
- 로직 금지
- 요청된 주문만 실행

---

# 11. System Identity

BlackTile V12는 다음과 같다:

> “자동매매 프로그램”이 아니라  
> “규칙 기반 트레이딩 엔진”

---

# 12. Success Definition

성공 기준:

- 안정적 24/7 운영
- 손실 제어 유지
- 백테스트와 실거래 일치
- 감정 개입 0%
- 시스템 기반 거래 유지
