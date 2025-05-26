# Project Activity Logs
- 이 문서는 `.cursor\rules\prjrule-record-today-logs.mdc`에 의해 자동 생성됩니다. 
> *Cursor AI* 등을 사용하여 IDE (Code Editor) 상에서 수행한 개발 기록 및 Prompt/Chat 내용을 바탕으로 자동 작성하는 것을 권장합니다.

## 2024-05-26

### 17:00 프로젝트 기술스택 및 구조 세팅
- Express.js, PostgreSQL, dotenv, React, Tailwind CSS, Jest, EsLint 등 기술스택 확정
- Context7 기반으로 의존성 설치 및 주요 설정 파일 자동 생성
- backend, frontend, user-documents 등 폴더 구조 개편 및 생성
- 주요 엔트리포인트, 테스트, 품질관리 파일 생성
- .env 파일 직접 생성 필요 안내 및 README에 관리법 추가 예정
- tailwind.config.js 파일 문법 오류 발견, 수정 예정

### 17:30 Vite 기반 프론트엔드 세팅 및 구조 리팩토링
- frontend 폴더에 Vite 기반 React 프로젝트로 재구성
- Tailwind CSS 4.x + Vite + ESM 환경에 맞게 postcss.config.cjs, @tailwindcss/postcss 적용
- 루트에 남아있던 이전 tailwind.config.js, postcss.config.js 파일 삭제
- frontend 내 node_modules, postcss.config.cjs, tailwind.config.js 등 위치 정상화
- 불필요한 예제/템플릿 파일(react.svg, vite.svg 등)은 유지, 나머지 구조만 정리
- 백엔드: `node backend/index.js`, 프론트엔드: `cd frontend && npm run dev`로 실행 방식 변경
- 최신 프로젝트 구조 및 연결 방식, 마이그레이션 가이드 문서에 반영

### 18:10 루트 .gitignore 멀티 패키지 구조 반영 및 최신화
- 백엔드/프론트엔드 멀티 패키지(모노레포) 구조에 맞게 루트 .gitignore 파일을 최신화
- node_modules, 환경설정, 빌드 산출물, OS/IDE 파일, 백엔드/프론트엔드 전용 무시 규칙 등 통합 관리
- 기존 단일 node_modules 무시 규칙에서 전체 폴더 및 하위 폴더별 무시 규칙으로 확장

## 2024-03-21

### 15:45 README.md 파일 업데이트
- 프로젝트 구조 섹션에 상세 주석 추가
  - 백엔드/프론트엔드 디렉토리 구조 설명
  - 각 폴더와 파일의 역할 및 용도 설명
- 설치 및 실행 섹션 구조 개선
  - 사전 준비 항목 번호 수정 (0번으로 시작)
  - 설치 단계 명확화

### 15:40 Cursor Rules 파일 경로 수정
- `.cursor/rules/prjrule-new-feature-added.mdc` 파일의 경로 참조 수정
  - 요구사항 문서 경로: `user-documents/requirements/requirements.md`
  - 테스트 시나리오 파일 경로: `user-documents/test_specification/tests.json`
  - 테스트 요구사항 문서 경로: `user-documents/02_test_requirements.md`

### 15:35 테스트 명세 파일 작성
- `user-documents/test_specification/tests.json` 파일에 Sample 테스트 시나리오 및 케이스 추가
  - 각 시나리오별 5개의 샘플 테스트 케이스 작성
  - 모든 샘플 케이스에 실제 검증 가능한 입력값과 기대결과 포함

### 15:30 테스트 요구사항 문서 업데이트
- `user-documents/02_test_requirements.md` 파일에 시나리오 수준의 사전조건 필드 추가
  - `scenario_precondition` 필드 추가: 시나리오 내 모든 테스트케이스가 공유하는 사전조건을 정의
  - 스키마 구조, 필드 작성법, 예시 등 문서 전체 업데이트
  - 개별 테스트케이스의 사전조건과 시나리오 수준의 사전조건을 구분하여 관리하도록 개선


