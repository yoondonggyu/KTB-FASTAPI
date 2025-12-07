# 🐾 동물 감정일기 - KakaoTech Bootcamp FastAPI Project

> **바닐라 JavaScript + FastAPI + AI 모델 서빙** 통합 커뮤니티 게시판

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](https://python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![JavaScript](https://img.shields.io/badge/Vanilla_JS-ES6+-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-FF6F00?logo=tensorflow&logoColor=white)](https://www.tensorflow.org/)
[![Gemini](https://img.shields.io/badge/Google-Gemini_API-4285F4?logo=google&logoColor=white)](https://ai.google.dev/)
[![Tests](https://img.shields.io/badge/Tests-263_cases-10B981?logo=pytest&logoColor=white)](./TEST_CASES_COMPLETE.html)

---

## 📋 프로젝트 소개

**동물 감정일기**는 **카카오테크 부트캠프 1기** FastAPI 프로젝트입니다.

이 저장소는 **마스터 노드(클러스터)** 역할을 하며, Frontend / Backend / Model 3개의 하위 프로젝트를 **Git Subtree**로 통합 관리합니다.

### 🎯 부트캠프 과제 요구사항

| # | 요구사항 | 상태 |
|---|----------|:----:|
| 1 | FastAPI 기반 REST API 서버 구현 | ✅ |
| 2 | **바닐라 JS 웹 프론트엔드**에서 FastAPI 모델 서빙 사용 | ✅ |
| 3 | AI 모델 연동 (이미지 분류 + 감정 분석) | ✅ |
| 4 | pytest 기반 테스트 케이스 작성 (263개) | ✅ |
| 5 | Git Repository README 프로젝트 문서화 | ✅ |

---

## 🏗 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────────────────┐
│                     🐾 KTB-FASTAPI (Master Repository)               │
│                         Git Subtree로 통합 관리                       │
└─────────────────────────────────────────────────────────────────────┘
                                    │
           ┌────────────────────────┼────────────────────────┐
           │                        │                        │
           ▼                        ▼                        ▼
┌─────────────────────┐  ┌─────────────────────┐  ┌─────────────────────┐
│  🌐 Frontend        │  │  🔧 Backend         │  │  🤖 Model           │
│  ─────────────────  │  │  ─────────────────  │  │  ─────────────────  │
│  Vanilla JS (ES6+)  │  │  FastAPI REST API   │  │  AI Model 서빙       │
│  HTML5 + CSS3       │  │  MySQL + SQLAlchemy │  │  Keras CNN          │
│  Fetch API          │  │  Session Auth       │  │  Google Gemini      │
│                     │  │                     │  │  Ollama LLM         │
│  📦 Port: 3000      │  │  📦 Port: 8000      │  │  📦 Port: 8001      │
└─────────────────────┘  └─────────────────────┘  └─────────────────────┘
           │                        │                        │
           └────────────────────────┴────────────────────────┘
                                    │
                                    ▼
                    ┌───────────────────────────────┐
                    │   💾 MySQL Database           │
                    │   FASTAPI_Project_DB          │
                    └───────────────────────────────┘
```

---

## 📁 저장소 구조

```
KTB-FASTAPI/                          # 🎯 마스터 저장소 (클러스터)
│
├── 📄 README.md                      # 프로젝트 통합 문서
├── 📊 TEST_CASES_COMPLETE.html       # 통합 테스트 케이스 문서
│
├── 🌐 Frontend/                      # Git Subtree: 프론트엔드
│   ├── index.html                    # SPA 메인 페이지
│   ├── css/index.css                 # 스타일시트
│   ├── js/                           # JavaScript 모듈
│   │   ├── api.js                    # API 통신
│   │   ├── auth.js                   # 인증 로직
│   │   └── posts.js                  # 게시글 로직
│   └── tests/                        # pytest 테스트 (100개)
│
├── 🔧 Backend/                       # Git Subtree: 백엔드 API
│   ├── app/
│   │   ├── main.py                   # FastAPI 앱
│   │   ├── routers/                  # API 라우터
│   │   ├── controllers/              # 비즈니스 로직
│   │   ├── models/                   # SQLAlchemy 모델
│   │   └── schemas.py                # Pydantic 스키마
│   └── tests/                        # pytest 테스트 (80개)
│
└── 🤖 Model/                         # Git Subtree: AI 모델 서빙
    ├── app/
    │   ├── main.py                   # FastAPI 앱
    │   ├── routers/
    │   │   ├── predict_routes.py     # 이미지 분류 API
    │   │   ├── sentiment_routes.py   # 감정 분석 API
    │   │   └── chat_routes.py        # LLM 채팅 API
    │   └── services/
    │       ├── model_service.py      # Keras 모델
    │       └── gemini_service.py     # Gemini API
    └── tests/                        # pytest 테스트 (83개)
```

---

## 🔗 하위 저장소 (Subtrees)

| 디렉토리 | 저장소 | 설명 |
|----------|--------|------|
| `Frontend/` | [KakaoTechBootcamp-Frontend](https://github.com/yoondonggyu/KakaoTechBootcamp-Frontend) | 바닐라 JS 웹 UI |
| `Backend/` | [KakaoTechBootcamp-Backend](https://github.com/yoondonggyu/KakaoTechBootcamp-Backend) | FastAPI REST API |
| `Model/` | [KakaoTechBootcamp-Model](https://github.com/yoondonggyu/KakaoTechBootcamp-Model) | AI 모델 서빙 |

---

## ✨ 주요 기능

### 🌐 프론트엔드 (Vanilla JS)

- 회원가입 / 로그인 (세션 기반 인증)
- 게시글 CRUD + 이미지 업로드
- 댓글 CRUD + 감정 분석 표시
- 좋아요 / 조회수

### 🔧 백엔드 API (FastAPI)

- RESTful API 설계
- MySQL + SQLAlchemy ORM
- Pydantic 유효성 검사
- CORS 미들웨어

### 🤖 AI 모델 서빙 (FastAPI)

| 기능 | 입력 | 출력 | 기술 |
|------|------|------|------|
| **이미지 분류** | 이미지 파일 | 🐕 Dog / 🐈 Cat | Keras CNN |
| **감정 분석** | 텍스트 (한글/영어) | 😊 긍정 / 😞 부정 / 😐 중립 | Gemini API |
| **LLM 채팅** | 메시지 | 스트리밍 응답 | Ollama |

---

## 🧪 테스트 현황

| 서비스 | 테스트 수 | 결과 | 통과율 |
|--------|----------|------|--------|
| **Backend** | 80개 | ✅ 80 Pass | 100% |
| **Model** | 83개 | ✅ 65 Pass + ⏭️ 18 Skip | 78.3% |
| **Frontend** | 100개 | ✅ 100 Pass | 100% |
| **전체** | **263개** | **245 Pass** | **93.2%** |

### 📋 테스트 문서 (v4 최신본)

| 문서 | 설명 | 링크 |
|------|------|------|
| **Index** | 전체 테스트 개요 | [TEST_CASES_v4_index.html](./TEST_CASES_v4_index.html) |
| **Backend** | 백엔드 API 테스트 (80개) | [TEST_CASES_v4_backend.html](./TEST_CASES_v4_backend.html) |
| **Model** | AI 모델 테스트 (83개) | [TEST_CASES_v4_model.html](./TEST_CASES_v4_model.html) |
| **Frontend** | 프론트엔드 테스트 (100개) | [TEST_CASES_v4_frontend.html](./TEST_CASES_v4_frontend.html) |
| **Manual** | 수동 테스트 시나리오 | [TEST_CASES_v4_manual.html](./TEST_CASES_v4_manual.html) |

---

## 🚀 빠른 시작

### 1️⃣ 저장소 클론

```bash
git clone https://github.com/yoondonggyu/KTB-FASTAPI.git
cd KTB-FASTAPI
```

### 2️⃣ Backend 서버 실행 (포트 8000)

```bash
cd Backend
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # DATABASE_URL 설정
uvicorn app.main:app --reload --port 8000
```

### 3️⃣ Model 서버 실행 (포트 8001)

```bash
cd Model
pip install -r requirements.txt
cp .env.example .env  # GEMINI_API_KEY 설정
uvicorn app.main:app --reload --port 8001
```

### 4️⃣ Frontend 실행 (포트 3000)

```bash
cd Frontend
python -m http.server 3000
```

### 5️⃣ 브라우저 접속

```
http://localhost:3000
```

---

## 🛠 기술 스택

### Frontend
| 분류 | 기술 |
|------|------|
| Language | Vanilla JavaScript (ES6+) |
| Markup | HTML5, CSS3 |
| HTTP Client | Fetch API |

### Backend
| 분류 | 기술 |
|------|------|
| Framework | FastAPI 0.104+ |
| Language | Python 3.10+ |
| Database | MySQL 8.0 |
| ORM | SQLAlchemy 2.0 |

### AI/ML
| 분류 | 기술 |
|------|------|
| 이미지 분류 | TensorFlow / Keras |
| 감정 분석 | Google Gemini 2.5 Flash |
| LLM | Ollama (gemma3:4b) |

---

## 📚 Git Subtree 관리

### Subtree 추가 방법

```bash
# Frontend 추가
git subtree add --prefix=Frontend https://github.com/yoondonggyu/KakaoTechBootcamp-Frontend.git main --squash

# Backend 추가
git subtree add --prefix=Backend https://github.com/yoondonggyu/KakaoTechBootcamp-Backend.git main --squash

# Model 추가
git subtree add --prefix=Model https://github.com/yoondonggyu/KakaoTechBootcamp-Model.git main --squash
```

### Subtree 업데이트

```bash
# 하위 저장소 최신 변경사항 가져오기
git subtree pull --prefix=Frontend https://github.com/yoondonggyu/KakaoTechBootcamp-Frontend.git main --squash
git subtree pull --prefix=Backend https://github.com/yoondonggyu/KakaoTechBootcamp-Backend.git main --squash
git subtree pull --prefix=Model https://github.com/yoondonggyu/KakaoTechBootcamp-Model.git main --squash
```

### Subtree 변경사항 푸시

```bash
# 마스터에서 수정한 내용을 하위 저장소로 푸시
git subtree push --prefix=Frontend https://github.com/yoondonggyu/KakaoTechBootcamp-Frontend.git main
```

---

## 👨‍💻 개발자

- **윤동규** (Yoon Dong-Gyu)
- GitHub: [@yoondonggyu](https://github.com/yoondonggyu)
- **KakaoTech Bootcamp 1기**

---

## 🔮 추후 업그레이드 계획 (Roadmap)

**"반려동물과 나의 감정 교감 일기"**로 서비스의 정체성을 강화하고, 단순 기록을 넘어 **공감과 치유**를 제공하는 플랫폼으로 발전시킵니다.

### 1. 💌 듀얼 감정 트래킹 (Dual Emotion Tracking)
- **기능**: 반려동물의 사진으로 분석된 감정뿐만 아니라, **보호자의 오늘 하루 감정(텍스트/음성)**도 함께 기록합니다.
- **가치**: "나의 우울함이 강아지에게 영향을 주었을까?"와 같은 감정적 상호작용을 시각화합니다.

### 2. ❤️ 감정 공명 점수 (Resonance Score)
- **기능**: 반려인과 반려동물의 감정 데이터를 분석하여 **감정 일치도**와 **교감 지수**를 리포트로 제공합니다.
- **AI 활용**: LLM을 통해 "오늘 댕댕이가 주인님의 행복한 기분을 알아채고 더 신나했네요!" 같은 **감성 코멘트** 생성.

### 3. 🧩 맞춤형 힐링 추천 (Context-Aware Recommendations)
- **기능**: 현재의 듀얼 감정 상태에 딱 맞는 활동을 추천합니다.
    - *주인(피곤) + 강아지(심심)* 👉 "집에서 할 수 있는 노즈워크 놀이 3가지"
    - *주인(우울) + 강아지(행복)* 👉 "강아지의 해피 바이러스를 전수받는 가벼운 산책 코스"

### 4. 🏘️ 공감 커뮤니티 (Empathy Community)
- **기능**: 나와 비슷한 감정 패턴을 가진 보호자들을 매칭하거나 그룹화합니다.
- **예시**: "육아 스트레스를 겪는 초보 견주 모임", "노견과 함께하는 차분한 일상 공유"

### 5. 🎥 멀티모달 AI 확장 (Multimodal AI)
- **기능**: 사진뿐만 아니라 **짖는 소리(Audio)**나 **행동 영상(Video)**을 분석하여 더 정확한 감정과 의사를 파악합니다.

---

## 📝 라이선스

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <b>🐾 동물 감정일기 - KakaoTech Bootcamp FastAPI Project</b><br>
  Made with ❤️ by yoon-dong-gyu
</p>
