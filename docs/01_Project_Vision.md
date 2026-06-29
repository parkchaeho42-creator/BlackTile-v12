# BlackTile V12 - Project Vision

**Document ID:** 01  
**Version:** V12.0  
**Status:** Official  
**Last Updated:** 2026-06-29

---

# 1. Purpose

BlackTile V12는 Binance USDT-M Futures의 BTCUSDT Perpetual 전용 자동매매 시스템이다.

본 프로젝트는 단순한 자동매매 프로그램이 아니라, 장기간 안정적으로 운영 가능한 자동매매 플랫폼 구축을 목표로 한다.

---

# 2. Vision

하나의 코드베이스로 다음 환경을 모두 지원하는 자동매매 시스템을 구축한다.

- Backtest
- Paper Trading
- Shadow Live
- Live Trading

모든 환경은 동일한 거래 로직을 사용하며, 실행 환경만 변경한다.

---

# 3. Project Scope

## In Scope

- Binance USDT-M Futures
- BTCUSDT Perpetual
- Python 3.11+
- Google Colab 개발 환경
- Ubuntu Mini PC 운영 환경
- AI 기반 보조 분석
- 자동 리스크 관리
- 실시간 데이터 처리
- 백테스트 및 페이퍼 트레이딩

## Out of Scope

- 현물 거래
- 옵션 거래
- 다중 거래소 지원
- 다중 종목 지원
- 모바일 애플리케이션

---

# 4. Objectives

본 프로젝트의 핵심 목표는 다음과 같다.

1. 안정적인 자동매매 엔진 구축
2. 유지보수가 쉬운 Cell 기반 구조 설계
3. Backtest와 Live 간 동일한 실행 로직 유지
4. 리스크 관리 자동화
5. AI 기반 보조 의사결정 기능 제공
6. Mini PC 기반 24시간 운영

---

# 5. Design Principles

BlackTile V12는 다음 원칙을 따른다.

- One Cell = One Responsibility
- One Cell = One Python File
- Documentation First
- Test First
- Configuration Driven
- Fail Safe
- AI Assist Only
- Single Source of Truth

---

# 6. Success Criteria

프로젝트는 아래 조건을 만족하면 성공으로 정의한다.

- 모든 Cell 구현 완료
- Unit Test 통과
- Integration Test 통과
- Backtest 완료
- Paper Trading 완료
- Shadow Live 검증 완료
- Live Trading 안정 운영

---

# 7. Non-Functional Requirements

- 높은 안정성
- 높은 가독성
- 높은 확장성
- 높은 유지보수성
- 낮은 결합도
- 빠른 장애 복구

---

# 8. Target Environment

| Item | Value |
|------|-------|
| Exchange | Binance USDT-M Futures |
| Symbol | BTCUSDT Perpetual |
| Language | Python 3.11+ |
| Development | Google Colab |
| Production | Ubuntu Mini PC |

---

# 9. Project Philosophy

자동매매는 높은 수익보다 안정적인 운영을 우선한다.

모든 의사결정은 재현 가능해야 하며, 모든 실행은 기록되어야 한다.

AI는 보조 역할만 수행하며, 최종 거래 결정은 시스템 규칙에 따른다.

---

# 10. Version Policy

V12는 단일 거래소, 단일 종목에 집중한다.

향후 버전에서 다중 종목 및 다중 거래소를 지원할 수 있으나, V12에서는 범위를 확장하지 않는다.
