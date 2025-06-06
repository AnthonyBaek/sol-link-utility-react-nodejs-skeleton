# 프로젝트 요구사항 명세서

---

## 1. 프로젝트 개요
- 본 문서는 프로젝트의 모든 요구사항(기능/비기능)을 체계적으로 관리하기 위한 공식 문서입니다.
- 본 프로젝트는 다양한 유틸리티 기능을 제공하는 SPA 기반 웹 시스템(Utility Web Application, UTL)입니다.
    - 유틸리티 목록에 각 개발자가 설계한 도구를 포함시킬 수 있습니다.

---

## 2. 유틸리티(애플리케이션/시스템/모듈) 정의

- 현재는 ***UTL***이 N개의 유틸리티를 wrapping하고 있습니다.
- 개발 및 포함된(될) 유틸리티를 아래에 정의하고, 각 유틸리티의 약어를 영문 대문자 3자리로 명명하고, 아래의 테이블을 적절히 업데이트합니다.

| 약어 | 명칭(한글) | 명칭(영문) | 설명 |
|------|------------|------------|------|
| UTL  | 유틸리티 웹 애플리케이션 | Utility Web Application | 다양한 유틸리티 기능을 제공하는 SPA 기반 웹 시스템으로써, 다수 유틸리티/애플리케이션을 wrapping하는 역할을 수행하고, 공통된 UI/UX를 제공합니다. |

---

## 3. UTL 요구사항

### 3.1 UTL 기능 요구사항 (Functional Requirements, FR)
- **[UTL_FR_0001] 유틸리티 선택 드롭다운**
  - [UTL_FR_0001_01] 상단 바에서 유틸리티를 선택할 수 있는 드롭다운을 제공한다.
  - [UTL_FR_0001_02] 사용자는 드롭다운에서 유틸리티를 선택하여 각 유틸리티별 단일 작업 페이지로 이동할 수 있다.
  - [UTL_FR_0001_03] 선택된 유틸리티에 따라 작업 영역이 동적으로 변경된다.
- **[UTL_FR_0002] 툴 버튼 및 Side Peek**
  - [UTL_FR_0002_01] 상단 바 우측에 툴 버튼(T₁, T₂, T₃ 등)을 제공한다.
  - [UTL_FR_0002_02] 툴 버튼 클릭 시 우측에 Side Peek(툴 상세/컨트롤러) 영역이 슬라이드로 열린다.
  - [UTL_FR_0002_03] Side Peek는 닫기/너비조절 핸들을 제공한다.
- **[UTL_FR_0003] 섹션별 작업 및 컨트롤**
  - [UTL_FR_0003_01] 작업 영역은 여러 섹션(Accordion)으로 구성할 수 있다.
  - [UTL_FR_0003_02] 각 섹션별로 컨트롤 버튼 그룹을 제공한다.
  - [UTL_FR_0003_03] 섹션은 접기/펼치기(Accordion) 기능을 지원한다.
- **[UTL_FR_0004] SPA 및 동적 반영**
  - [UTL_FR_0004_01] 모든 주요 인터랙션(툴 선택, 섹션 토글 등)은 SPA 방식으로 즉시 반영되어야 한다.
- **[UTL_FR_0005] 데이터 시각화 및 접근**
  - [UTL_FR_0005_01] Source (DB, 파일 등)로부터 로드된 다수의 데이터는 그리드/테이블 뷰 형식으로 출력한다. (특정 DB에 대해 특수한 뷰(카드뷰, 타임라인뷰 등)를 사용할 경우 별도 요구사항으로 정의)

### 3.2 UTL 비기능 요구사항 (Non-Functional Requirements, NFR)

- [UIUX] **UI/UX 레이아웃 및 인터랙션**
  - [UTL_NFR_UIUX_0001] 공통 레이아웃: 상단 바(`로고`, `유틸리티 선택` 드롭다운, `유틸리티 툴` 버튼그룹), `작업 영역`, 스크롤바 등 공통 레이아웃을 갖는다.
    - [UTL_NFR_UIUX_0001_01] 메인 화면 이동: 로고를 클릭했을 때, 해당 유틸리티의 메인 화면으로 이동하며 열려있던 Side peek 등은 모두 닫힌다.
    - [UTL_NFR_UIUX_0001_02] 특정 유틸리티를 선택했을 경우, 해당 유틸리티 화면이 `작업영역`에 열리고, 해당 유틸리티에 대해 operation을 수행할 수 있는 버튼 그룹을 출력한다.
  - [UTL_NFR_UIUX_0002] 단일 페이지 구성: 각 유틸리티별 작업 영역은 단일 페이지로 구성한다.
  - [UTL_NFR_UIUX_0003] 섹션별 작업 및 컨트롤: 섹션별 작업(Accordion), 섹션별 컨트롤 버튼 그룹 제공, 섹션 접기/펼치기 지원
  - [UTL_NFR_UIUX_0004] Side Peek 인터랙션: `유틸리티 툴` 버튼 클릭 시 Side Peek(툴 상세/컨트롤러) 영역이 우측에 슬라이드로 열리고, 닫기/너비조절 핸들 제공
    - [UTL_NFR_UIUX_0004_01] `유틸리티 툴`은 각자 기능을 수행하는 화면과 컨트롤 버튼 등이 존재할 수 있으며, 이는 각 유틸리티 및 툴에 따라 상이하므로 요구사항에 따라 구현
    - [UTL_NFR_UIUX_0004_02] Side Peek의 너비를 조절할 경우, 너비에 맞게 Side Peek이 반응형 UI를 제공할 수 있어야 함
  - [UTL_NFR_UIUX_0005] SPA 및 즉시 반영: 모든 주요 인터랙션(툴 선택, 섹션 토글 등)은 SPA 방식으로 즉시 반영되어야 한다.
  - [UTL_NFR_UIUX_0006] 스크롤바 자동 표시: 작업 컨텐츠 크기에 따라 스크롤바가 자동 표시되어야 한다.
  - [UTL_NFR_UIUX_0007] 반응형 및 접근성: UI/UX는 반응형(Responsive)으로 설계되어야 하며, 접근성(Accessibility)도 고려한다.

- [VIS] **데이터 시각화**
  - [UTL_NFR_VIS_0001] 데이터베이스/CSV 기준의 데이터를 출력하는 경우, UTL 내부의 모든 유틸리티에 대해 동일한 UI의 깔끔한 그리드 스타일을 제공한다.


---

## 4. 요구사항 관리 이력
| 버전 | 일자 | 작성자 | 변경/추가 내용 |
|-------|------|--------|----------------|
| 0.6   | 2024-05-26 | Agent | 프로젝트 기술스택(Express.js, PostgreSQL, dotenv, React, Tailwind CSS, Jest, EsLint) 확정 및 Context7 기반 세팅, 폴더 구조 개편, 주요 설정/엔트리포인트/테스트/품질관리 파일 생성, .env 관리 가이드 추가 |
| 0.5   | 2024-03-21 | Agent | 데이터 시각화 및 접근(UTL_FR_0005, UTL_NFR_VIS_0001) 등 기능/비기능 요구사항 추가 및 ID 부여, UI/UX 요구사항 세분화 |
| 0.4   | 2024-03-21 | Agent | 모든 기능/비기능 요구사항 하위 항목에 ID 부여 및 계층적 분해, 비기능 요구사항 세부화, 작성 가이드 최신화 |
| 0.3   | 2024-03-21 | Agent | 요구사항을 bullet 계층형으로 분해, 하위 요구사항 ID 부여, 표 대신 bullet 구조로 변경 |
| 0.2   | 2024-03-21 | Agent | 프로젝트 개요, 유틸리티 정의, 기능/비기능 요구사항 구분, 표/구조/작성 가이드 반영 |
| 0.1   | 2024-03-21 | Agent | 최초 작성 |

> **요구사항 관리 이력은 에이전트가 자동으로 업데이트합니다.**

---

### 작성 가이드
- 요구사항 추가 시 반드시 ID, 명칭, 상세설명, 관련 테스트 ID/명을 기입
- 하위 요구사항 분해 시 ID 체계 준수
- 비기능 요구사항에는 UI/UX, 성능, 보안, 접근성 등 포함
- 테스트 명세와 상호참조 필수
