# BlackTile V12 - Master Index

**Document ID:** 00  
**Version:** V12.0  
**Status:** Official

---

# Purpose

이 문서는 BlackTile V12 프로젝트의 모든 공식 문서를 관리하는 최상위 인덱스이다.

모든 개발은 본 문서에서 정의한 문서 체계를 기준으로 진행한다.

---

# Documentation Structure

| ID | Document | Description | Status |
|----|----------|-------------|--------|
| 00 | Master Index | 문서 관리 및 목차 | ✅ |
| 01 | Project Vision | 프로젝트 목표 및 범위 | ⬜ |
| 02 | System Architecture | 전체 시스템 구조 | ⬜ |
| 03 | Development Standards | 개발 규약 | ⬜ |
| 04 | Common Data Models | 공통 데이터 모델 | ⬜ |
| 05 | Project Structure | 프로젝트 디렉터리 구조 | ⬜ |
| 06 | Config Specification | 설정 파일 명세 | ⬜ |
| 07 | Cell Architecture | Cell 기반 아키텍처 | ⬜ |
| 08 | Development Roadmap | 개발 단계 및 일정 | ⬜ |
| 09 | Testing Strategy | 테스트 전략 | ⬜ |
| 10 | Deployment Guide | 배포 및 운영 | ⬜ |
| 11 | AI Integration | AI 통합 규칙 | ⬜ |
| 12 | Git Workflow | Git 운영 규칙 | ⬜ |
| 13 | Coding Conventions | 코딩 스타일 및 네이밍 | ⬜ |
| 14 | Changelog | 변경 이력 | ⬜ |

---

# Reading Order

새로운 개발자는 아래 순서로 문서를 읽는다.

1. Master Index
2. Project Vision
3. System Architecture
4. Development Standards
5. Common Data Models
6. Project Structure
7. Config Specification
8. Cell Architecture
9. Development Roadmap
10. Testing Strategy
11. Deployment Guide
12. AI Integration
13. Git Workflow
14. Coding Conventions

---

# Development Flow

```
Project Vision
        │
        ▼
Architecture
        │
        ▼
Development Standards
        │
        ▼
Common Data Models
        │
        ▼
Project Structure
        │
        ▼
Config Specification
        │
        ▼
Cell Architecture
        │
        ▼
Coding
        │
        ▼
Testing
        │
        ▼
Deployment
```

---

# Documentation Rules

- 모든 문서는 Markdown(.md) 형식으로 작성한다.
- 문서 번호(ID)는 변경하지 않는다.
- 문서를 수정할 경우 CHANGELOG에 기록한다.
- 설계 변경은 문서를 먼저 수정한 후 코드를 수정한다.
- 문서와 코드의 불일치를 허용하지 않는다.
