# BlackTile V12 - System Architecture

**Document ID:** 02  
**Version:** V12.0  
**Status:** Official  
**Last Updated:** 2026-06-29

---

# 1. Purpose

본 문서는 BlackTile V12의 전체 시스템 구조와 각 계층의 역할을 정의한다.

모든 구현은 본 문서에서 정의한 아키텍처를 기준으로 개발한다.

---

# 2. Architecture Principles

BlackTile V12는 다음 원칙을 따른다.

- Single Responsibility Principle
- One Cell = One Python File
- One Cell = One Main Class
- Layered Architecture
- Unidirectional Dependency
- Documentation First
- Test First
- Fail Safe Design

---

# 3. High-Level Architecture

```
Bootstrap
        │
        ▼
Data Pipeline
        │
        ▼
Indicator Engine
        │
        ▼
Strategy Engine
        │
        ▼
Risk Engine
        │
        ▼
Decision Engine
        │
        ▼
Execution Engine
        │
        ▼
Protection Engine
        │
        ▼
Database & Analytics
        │
        ▼
AI Engine
        │
        ▼
BlackTile Engine
```

---

# 4. Layer Responsibilities

## Bootstrap

프로젝트 초기화 및 환경 준비

---

## Data Pipeline

실시간 데이터 수집 및 정규화

---

## Indicator Engine

기술지표 계산

---

## Strategy Engine

매매 신호 생성

---

## Risk Engine

리스크 계산 및 거래 가능 여부 판단

---

## Decision Engine

최종 거래 승인

---

## Execution Engine

주문 생성 및 실행

---

## Protection Engine

장애 감지 및 시스템 보호

---

## Database & Analytics

로그 저장 및 성과 분석

---

## AI Engine

시장 분석 및 추천값 생성

AI는 직접 주문하지 않는다.

---

## BlackTile Engine

각 계층을 연결하는 오케스트레이터이다.

비즈니스 로직을 포함하지 않는다.

---

# 5. Dependency Rules

의존성은 항상 상위 계층에서 하위 계층으로만 허용한다.

순환 참조(Circular Dependency)는 허용하지 않는다.

---

# 6. Data Flow

```
Market Data
      │
      ▼
Indicators
      │
      ▼
Strategy
      │
      ▼
Risk
      │
      ▼
Decision
      │
      ▼
Execution
      │
      ▼
Protection
      │
      ▼
Database
```

---

# 7. Runtime Modes

동일한 엔진으로 아래 실행 모드를 지원한다.

- Backtest
- Paper Trading
- Shadow Live
- Live Trading

환경에 따라 데이터 입력과 주문 실행 방식만 변경한다.

---

# 8. Error Handling

모든 계층은 예외를 처리하고 Logger를 통해 기록한다.

치명적인 오류 발생 시 Protection Engine이 시스템을 안전하게 중지한다.

---

# 9. Extensibility

새로운 전략이나 AI 모듈은 기존 Cell을 수정하지 않고 새로운 Cell을 추가하는 방식으로 확장한다.

---

# 10. Architecture Rules

- 계층 간 책임을 침범하지 않는다.
- Engine은 연결만 수행한다.
- AI는 보조 역할만 수행한다.
- 모든 실행은 Logger에 기록한다.
- 모든 데이터는 공통 데이터 모델을 사용한다.
