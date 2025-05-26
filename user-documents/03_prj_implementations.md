# 실질적 구현 방안 및 프로젝트 세팅 전략

## 1. 백엔드 (Express.js + PostgreSQL + dotenv)

### 1.1. Express.js 서버
- `backend/index.js`에서 Express 앱 생성, JSON 파싱 미들웨어 적용
- API 엔드포인트 예시: `/api/utilities`, `/api/data`
- CORS 설정 필요시 `cors` 미들웨어 추가

### 1.2. PostgreSQL 연동
- `pg` 패키지로 DB Pool 생성 (`backend/db.js`)
- 쿼리 함수 export, 각 API 라우트에서 import하여 사용
- 환경변수(`.env`)로 DB 접속 정보 관리

### 1.3. dotenv
- `backend/index.js` 최상단에서 `require('dotenv').config()` 호출
- `.env` 파일에 DB, 포트 등 민감 정보 저장

## 2. 프론트엔드 (React + Tailwind CSS)

### 2.1. React
- `frontend/src/App.jsx`에서 SPA 구조 설계
- 주요 컴포넌트: 상단바, 유틸리티 드롭다운, 섹션(Accordion), Side Peek 등
- API 호출은 `fetch` 또는 `axios` 사용

### 2.2. Tailwind CSS
- `frontend/tailwind.config.js`에서 경로 지정
- `frontend/postcss.config.js`에 Tailwind 플러그인 추가
- `frontend/src/styles/index.css`에 Tailwind base, components, utilities import
- 컴포넌트 내에서 Tailwind 유틸리티 클래스 적극 활용

## 3. 테스트 (Jest)
- `backend/tests/`, `frontend/src/tests/` 폴더 또는 `*.test.js(x)` 파일에 테스트 작성
- 백엔드: API 단위 테스트 (supertest 활용 가능)
- 프론트엔드: 컴포넌트 렌더링/동작 테스트 (jest + @testing-library/react)
- `jest.config.js`에서 환경별 세팅

## 4. 코드 품질 (ESLint)
- `.eslintrc.js`에 React, Node, Jest 플러그인 및 룰 적용
- `eslint --fix`로 자동 포맷팅 가능
- CI/CD 연동 시 lint 단계 추가 권장

## 5. 실행 및 개발 플로우
1. **의존성 설치**
   - `npm install express pg dotenv react react-dom tailwindcss postcss autoprefixer jest eslint @testing-library/react`
2. **백엔드 실행**
   - `node backend/index.js` (혹은 nodemon)
3. **프론트엔드 개발**
   - `npm run start` (React 개발 서버)
4. **테스트 실행**
   - `npm test`
5. **Lint 실행**
   - `npx eslint .`

## 6. 실질적 구현 방안 요약
- **SPA 구조**: React로 UI/UX 요구사항(드롭다운, Side Peek, 섹션 등) 구현, Tailwind로 반응형/접근성 강화
- **API 설계**: Express에서 RESTful 엔드포인트 제공, PostgreSQL과 연동
- **환경변수 관리**: dotenv로 민감 정보 분리
- **테스트/품질**: Jest로 TDD, ESLint로 코드 일관성 유지
- **문서/로그/요구사항**: 기존 `user-documents` 체계와 연동하여 요구사항 기반 개발 및 추적성 확보

## Tailwind CSS 4.x + Vite + ESM 환경 마이그레이션 가이드

- Tailwind CSS 4.x부터 PostCSS 플러그인이 별도 패키지(@tailwindcss/postcss)로 분리됨
- Vite(React) + ESM 환경에서는 postcss.config.cjs로 작성해야 하며, 아래와 같이 설정

```js
// frontend/postcss.config.cjs
module.exports = {
  plugins: {
    '@tailwindcss/postcss': {},
    autoprefixer: {},
  },
};
```
- 반드시 @tailwindcss/postcss를 devDependencies로 설치해야 함
- 공식 가이드: https://tailwindcss.com/docs/upgrade-guide#postcss

## Vite 기준 백엔드/프론트엔드 실행 방법

- 백엔드: `node backend/index.js`
- 프론트엔드: `cd frontend && npm run dev` (PowerShell: `cd frontend; npm run dev`)
- 개발 시 포트가 다르므로, API 호출 시 CORS 허용 필요
- 운영 배포 시에는 Nginx/Proxy 등으로 통합 가능

## 최신 프로젝트 구조 (Vite 기반)

```plaintext
/프로젝트_루트
│
├─ backend/                        # 백엔드(Express, DB) 관련 소스
│    ├─ index.js                   # Express 서버 엔트리포인트
│    ├─ db.js                      # PostgreSQL 연결 및 쿼리 함수
│
├─ frontend/                       # 프론트엔드(React, Tailwind, Vite)
│    ├─ src/                       # (Vite 템플릿 구조, 예제 파일 일부 유지)
│    ├─ public/
│    ├─ node_modules/
│    ├─ package.json
│    ├─ package-lock.json
│    ├─ postcss.config.cjs
│    ├─ tailwind.config.js
│    ├─ vite.config.ts
│    ├─ tsconfig.json (TypeScript 지원, JS만 쓸 거면 삭제 가능)
│    ├─ tsconfig.node.json
│    ├─ tsconfig.app.json
│    ├─ eslint.config.js
│    └─ README.md
│
├─ node_modules/                   # 루트 공통 의존성
├─ package.json                    # 루트 공통 의존성
├─ package-lock.json
├─ jest.config.ts                  # 공통 테스트 설정
├─ eslint.config.mjs               # 공통 린트 설정
│
├─ user-documents/                 # 요구사항, 명세, 로그 등 프로젝트 문서
│    ├─ 01_prj_requirements.md
│    ├─ 02_test_requirements.md
│    ├─ 03_prj_implementations.md
│    ├─ test_specification/
│    │    └─ tests.json
│    └─ logs/
│         └─ prj_logs.md
│
└─ README.md                       # 프로젝트 개요 및 가이드
```

## 백엔드-프론트엔드 연결 방식

- **SPA-API 분리**: React(Vite) SPA와 Express API 서버를 분리하여 개발/운영
- **API 연동**: 프론트엔드에서 fetch/axios 등으로 `/api/` 엔드포인트 호출
- **CORS**: 개발 환경에서는 포트가 다르므로 백엔드에서 CORS 허용 필요
<!-- - **운영 배포**: Nginx/Proxy 등으로 SPA와 API를 하나의 도메인으로 통합 가능 -->
- **Context7 근거**:
  - SPA-API 분리 구조는 확장성, 유지보수성, 보안, CI/CD에 유리
  - 환경변수(.env)로 민감 정보 분리, 보안 강화
  - 프론트엔드와 백엔드가 독립적으로 테스트/배포 가능

> 본 문서는 Express.js, PostgreSQL, dotenv, React, Tailwind CSS, Jest, EsLint 기반 웹 유틸리티 프로젝트의 실질적 구현 방안을 체계적으로 기록한 자료입니다.

## 7. 개발 서버 실행 및 접근 방법 정리

- **프론트엔드 개발 서버(Vite)**:
  - `npm run dev` (또는 `cd frontend; npm run dev`)
  - 브라우저에서 `http://localhost:5173` (또는 5174)로 접속
  - 정상적으로 React SPA가 뜨고, 내부에서 API 호출은 `http://localhost:4000/api/...`로 요청

- **백엔드(Express) 서버**:
  - `node backend/index.js`
  - 브라우저에서 `http://localhost:4000/api/health` 등 API 엔드포인트만 응답
  - 브라우저에서 `http://localhost:4000`으로 직접 접속 시 404 Not Found가 뜨는 것이 정상 (API 전용 서버)

> 실제 개발/테스트는 반드시 Vite 개발 서버(5173/5174)로 접속하여 React SPA를 확인하고, API 요청만 4000 포트로 보내야 함을 명심하세요.
