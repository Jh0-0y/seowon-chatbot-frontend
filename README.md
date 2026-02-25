# Chat-OS — Seowon Chatbot Frontend

AI 챗봇 서비스 **Chat-OS**의 React 기반 프론트엔드입니다.

---

## 기술 스택

| 분류 | 기술 |
|---|---|
| UI | React 19, CSS Modules |
| 상태 관리 | Redux Toolkit, React Redux |
| 라우팅 | React Router DOM v7 |
| HTTP 통신 | Axios |
| 인증 | JWT (Bearer Token) |
| 빌드 도구 | CRACO (CRA 커스터마이징) |
| 테스트 | MSW (Mock Service Worker), Testing Library |

---

## 프로젝트 구조

```
src/
├── assets/
│   ├── icons/          # SVG 아이콘 컴포넌트
│   └── logo/           # 로고 이미지
├── components/
│   ├── chat/
│   │   ├── layout/     # ChatSideBar, ChatHeader, ChatContents, ChatBottom
│   │   └── ui/         # ChatBubble, DeleteModal, UserProfile, LogoutBtn
│   ├── login/
│   │   └── layout/     # LoginForm
│   └── register/
│       ├── layout/     # RegisterForm, RegisterStep
│       └── section/    # StepTerms, StepEmail, StepInfo, StepComplete
├── modules/
│   ├── auth/           # 로그인/회원가입 API, Redux 슬라이스, 훅
│   ├── chat/           # 채팅 API, Redux 슬라이스, 훅
│   └── shared/
│       ├── api/        # axiosInstance (인터셉터 포함)
│       ├── hooks/      # useIsMobile
│       ├── utils/      # localStorage, focusHelpers
│       └── store.js    # Redux 스토어
├── pages/
│   ├── ChatPage.jsx
│   ├── LoginPage.jsx
│   └── RegisterPage.jsx
└── routes/
    └── AppRouter.jsx
```

---

## 주요 기능

### 인증
- **로그인** — 이메일/비밀번호 기반 로그인, JWT 토큰 로컬스토리지 저장
- **회원가입** — 4단계 스텝 형태 (약관 동의 → 이메일 입력 → 정보 입력 → 완료)

### 채팅
- **채팅방 관리** — 생성, 목록 조회, 이름 수정, 삭제
- **대화 기록** — 세션별 이전 채팅 내역 불러오기
- **실시간 메시지** — 사용자 메시지 전송 및 AI 응답 수신

### UI/UX
- 사이드바를 통한 채팅방 전환
- 모바일 반응형 지원 (`useIsMobile` 훅)
- 채팅 상태를 로컬스토리지에 영속화

---

## API 명세

Base URL: `http://118.44.206.66:8080/api`

| 메서드 | 경로 | 설명 |
|---|---|---|
| POST | `/auth/login` | 로그인 |
| POST | `/auth/register` | 회원가입 |
| POST | `/chat` | 메시지 전송 |
| POST | `/session/create` | 채팅방 생성 |
| POST | `/session/list` | 채팅방 목록 조회 |
| GET | `/session/:id` | 채팅 내역 조회 |
| PUT | `/session/:id` | 채팅방 이름 수정 |
| DELETE | `/session/:id` | 채팅방 삭제 |

모든 인증이 필요한 요청에는 `Authorization: Bearer <token>` 헤더가 자동으로 추가됩니다.

---

## 시작하기

### 사전 요구사항

- Node.js 18+
- npm 또는 yarn

### 설치 및 실행

```bash
# 의존성 설치
npm install

# 개발 서버 실행 (http://localhost:3000)
npm start

# 프로덕션 빌드
npm run build

# 테스트 실행
npm test
```

### 경로 별칭

`craco.config.js`에 `@` → `src/` 별칭이 설정되어 있습니다.

```js
import SomeComponent from '@/components/...'
```

---

## 페이지 라우팅

| 경로 | 페이지 | 설명 |
|---|---|---|
| `/` | ChatPage | 메인 채팅 페이지 |
| `/auth/login` | LoginPage | 로그인 |
| `/auth/register` | RegisterPage | 회원가입 |
