# 🧪 FastAPI Project 테스트 케이스 문서 v4

> **작성일**: 2025-12-06  
> **버전**: 4.0.0  
> **작성자**: yoon-dong-gyu

---

## 📋 목차

1. [개요](#1-개요)
2. [테스트 환경](#2-테스트-환경)
3. [테스트 결과 요약](#3-테스트-결과-요약)
4. [Backend 테스트 케이스](#4-backend-테스트-케이스)
5. [Model 서버 테스트 케이스](#5-model-서버-테스트-케이스)
6. [Frontend 테스트 케이스](#6-frontend-테스트-케이스)
7. [테스트 실행 방법](#7-테스트-실행-방법)
8. [상세 문서 링크](#8-상세-문서-링크)

---

## 1. 개요

### 1.1 프로젝트 구조
```
FASTAPI_PROJECT_KTB/
├── FASTAPI_Project_back/    # 백엔드 API 서버 (Port 8000)
├── FASTAPI_Project_model/   # AI 모델 서빙 서버 (Port 8001)
└── FASTAPI_Project_front/   # 프론트엔드 (Vanilla JS)
```

### 1.2 테스트 목적
- API 엔드포인트 정상 동작 확인
- 입력 유효성 검사 검증
- 에러 처리 확인
- 인증/인가 동작 검증
- AI 모델 서빙 기능 확인

---

## 2. 테스트 환경

| 항목 | 버전/설정 |
|------|----------|
| **Python** | 3.10.19 |
| **pytest** | 9.0.1 |
| **FastAPI** | 0.100+ |
| **테스트 DB** | SQLite (in-memory) |
| **Conda 환경** | env_python310 |
| **Platform** | darwin (macOS) |

### 2.1 의존성 설치
```bash
pip install pytest pytest-asyncio httpx
```

---

## 3. 테스트 결과 요약

### 3.1 전체 통계

| 서비스 | 테스트 수 | 통과 | 스킵 | 통과율 |
|--------|----------|------|------|--------|
| **Backend** | 80 | 80 | 0 | ✅ 100% |
| **Model** | 83 | 65 | 18 | ⚠️ 78.3% |
| **Frontend** | 100 | 100 | 0 | ✅ 100% |
| **전체** | **263** | **245** | **18** | **93.2%** |

### 3.2 분류별 상세

#### Backend (80개)
| 분류 | 테스트 수 | 통과 | 상태 |
|------|----------|------|------|
| Auth (회원가입/로그인) | 17 | 17 | ✅ 100% |
| Posts (게시글 CRUD) | 34 | 34 | ✅ 100% |
| Comments (댓글 CRUD) | 15 | 15 | ✅ 100% |
| Users (사용자 관리) | 14 | 14 | ✅ 100% |

#### Model (83개)
| 분류 | 테스트 수 | 통과 | 스킵 | 상태 |
|------|----------|------|------|------|
| Ollama Chat | 10 | 2 | 8 | ⚠️ Ollama 필요 |
| Gemini Chat | 5 | 5 | 0 | ✅ 100% |
| Sentiment (감성분석) | 18 | 18 | 0 | ✅ 100% |
| Predict (이미지분류) | 7 | 7 | 0 | ✅ 100% |
| Summarization (요약) | 10 | 10 | 0 | ✅ 100% |
| System & WebSocket | 33 | 23 | 10 | ⚠️ WS 필요 |

#### Frontend (100개)
| 분류 | 테스트 수 | 통과 | 상태 |
|------|----------|------|------|
| Auth Validation | 26 | 26 | ✅ 100% |
| Posts Validation | 24 | 24 | ✅ 100% |
| Comments Validation | 22 | 22 | ✅ 100% |
| API Structure | 28 | 28 | ✅ 100% |

---

## 4. Backend 테스트 케이스

### 4.1 인증 (Auth) API - 17개

#### 회원가입 테스트 (9개)

| TC-ID | 테스트명 | 설명 | 예상 결과 | 상태 |
|-------|---------|------|----------|------|
| AUTH-001 | test_signup_success | 정상 회원가입 | 201 Created | ✅ |
| AUTH-002 | test_signup_without_profile | 프로필 이미지 없이 가입 | 201 Created | ✅ |
| AUTH-003 | test_signup_duplicate_email | 중복 이메일 | 400/409 Error | ✅ |
| AUTH-004 | test_signup_invalid_email_format | 잘못된 이메일 형식 | 400/422 Error | ✅ |
| AUTH-005 | test_signup_password_mismatch | 비밀번호 불일치 | 400 Error | ✅ |
| AUTH-006 | test_signup_missing_required_fields | 필수 필드 누락 | 422 Error | ✅ |
| AUTH-007 | test_signup_empty_nickname | 빈 닉네임 | 400/422 Error | ✅ |
| AUTH-008 | test_signup_invalid_profile_url | 잘못된 프로필 URL | 422 Error | ✅ |
| AUTH-009 | test_signup_weak_password | 약한 비밀번호 | 400 Error | ✅ |

#### 로그인 테스트 (8개)

| TC-ID | 테스트명 | 설명 | 예상 결과 | 상태 |
|-------|---------|------|----------|------|
| AUTH-010 | test_login_success | 정상 로그인 | 200 OK + token | ✅ |
| AUTH-011 | test_login_wrong_password | 잘못된 비밀번호 | 400/401 Error | ✅ |
| AUTH-012 | test_login_nonexistent_user | 미존재 사용자 | 400/401 Error | ✅ |
| AUTH-013 | test_login_invalid_email_format | 이메일 형식 오류 | 400/422 Error | ✅ |
| AUTH-014 | test_login_missing_password | 비밀번호 누락 | 422 Error | ✅ |
| AUTH-015 | test_login_missing_email | 이메일 누락 | 422 Error | ✅ |
| AUTH-016 | test_login_empty_credentials | 빈 자격 증명 | 400/422 Error | ✅ |
| AUTH-017 | test_login_empty_body | 빈 요청 본문 | 422 Error | ✅ |

### 4.2 게시글 (Posts) API - 34개

| TC-ID | 테스트명 | 설명 | 예상 결과 | 상태 |
|-------|---------|------|----------|------|
| POST-001 | test_get_posts_success | 게시글 목록 조회 | 200 OK | ✅ |
| POST-002 | test_get_posts_with_pagination | 페이지네이션 | 200 OK | ✅ |
| POST-003 | test_get_posts_with_board_type | 게시판 타입 필터 | 200 OK | ✅ |
| POST-004~007 | 페이지네이션 유효성 | page/limit 검증 | 200/422 | ✅ 4개 |
| POST-008~010 | 게시글 상세 조회 | 정상/미존재/잘못된ID | 200/404/422 | ✅ 3개 |
| POST-011~017 | 게시글 작성 | CRUD 전체 | 201/400/422 | ✅ 7개 |
| POST-018~021 | 게시글 수정/삭제 | 수정/권한/삭제 | 200/403/404 | ✅ 4개 |
| POST-022~024 | 좋아요/조회수/업로드 | 인터랙션 | 200/201 | ✅ 3개 |
| POST-025~034 | 추가 테스트 | 엣지 케이스 | 다양 | ✅ 10개 |

### 4.3 댓글 (Comments) API - 15개

| TC-ID | 테스트명 | 설명 | 예상 결과 | 상태 |
|-------|---------|------|----------|------|
| CMT-001~002 | 댓글 목록 조회 | 정상/잘못된 ID | 200/422 | ✅ 2개 |
| CMT-003~006 | 댓글 작성 | 미존재 게시글/인증/누락/빈값 | 201/401/404/422 | ✅ 4개 |
| CMT-007~010 | 댓글 수정 | 미존재/인증/누락 | 200/401/404/422 | ✅ 4개 |
| CMT-011~013 | 댓글 삭제 | 미존재/인증/미존재 게시글 | 200/401/404 | ✅ 3개 |
| CMT-014~015 | 통합 테스트 | CRUD 워크플로우 | 다양 | ✅ 2개 |

### 4.4 사용자 (Users) API - 14개

| TC-ID | 테스트명 | 설명 | 예상 결과 | 상태 |
|-------|---------|------|----------|------|
| USR-001~004 | 프로필 이미지 | PNG/JPEG/잘못된타입/없음 | 200/400/422 | ✅ 4개 |
| USR-005~007 | 닉네임 수정 | 정상/인증없음/빈값 | 200/401/422 | ✅ 3개 |
| USR-008~011 | 비밀번호 변경 | 정상/틀림/불일치/인증없음 | 200/400/401 | ✅ 4개 |
| USR-012~014 | 회원 탈퇴 | 정상/인증없음/추가 | 200/401 | ✅ 3개 |

---

## 5. Model 서버 테스트 케이스

### 5.1 채팅 API - 15개

#### Ollama Chat (10개) - ⚠️ 8개 스킵

| TC-ID | 테스트명 | 설명 | 상태 |
|-------|---------|------|------|
| CHAT-001 | test_chat_missing_message | message 필드 누락 | ✅ |
| CHAT-002 | test_chat_empty_body | 빈 요청 본문 | ✅ |
| CHAT-003~010 | Ollama 실제 테스트 | 스트리밍/모델 전환 등 | ⏭️ Skip |

> **Skip 원인**: Ollama 서비스 미실행 (Connection refused)  
> **해결**: `ollama serve` 실행 후 테스트

#### Gemini Chat (5개) - ✅ 100%

| TC-ID | 테스트명 | 설명 | 상태 |
|-------|---------|------|------|
| GEMINI-001 | test_gemini_chat_basic | 기본 채팅 | ✅ |
| GEMINI-002 | test_gemini_chat_korean | 한국어 채팅 | ✅ |
| GEMINI-003 | test_gemini_chat_with_history | 대화 기록 포함 | ✅ |
| GEMINI-004 | test_gemini_emotion | 감정 분석 채팅 | ✅ |
| GEMINI-005 | test_gemini_missing_message | 메시지 누락 | ✅ |

### 5.2 감성 분석 (Sentiment) API - 18개 ✅

| TC-ID | 테스트명 | 설명 | 상태 |
|-------|---------|------|------|
| SNT-001~003 | ML 감성분석 | positive/negative/explain | ✅ |
| SNT-004~007 | 에러 케이스 | 빈텍스트/공백/누락/긴텍스트 | ✅ |
| SNT-008~012 | Gemini 감성분석 | 한국어/영어/이모지/혼합 | ✅ |
| SNT-013~018 | 추가 테스트 | 엣지 케이스 | ✅ |

### 5.3 이미지 분류 (Predict) API - 7개 ✅

| TC-ID | 테스트명 | 설명 | 상태 |
|-------|---------|------|------|
| IMG-001 | test_predict_png | PNG 이미지 분류 | ✅ |
| IMG-002 | test_predict_jpeg | JPEG 이미지 분류 | ✅ |
| IMG-003 | test_predict_invalid_type | text/plain 거부 | ✅ |
| IMG-004 | test_predict_no_file | 파일 없음 | ✅ |
| IMG-005 | test_predict_empty_file | 빈 파일 | ✅ |
| IMG-006 | test_predict_gif_rejected | GIF 거부 | ✅ |
| IMG-007 | test_predict_corrupted | 손상된 이미지 | ✅ |

### 5.4 텍스트 요약 (Summarization) API - 10개 ✅

| TC-ID | 테스트명 | 설명 | 상태 |
|-------|---------|------|------|
| SUM-001~003 | 기본 요약 | 긴텍스트/짧은텍스트/빈텍스트 | ✅ |
| SUM-004~006 | 요약 옵션 | 누락/매우긴/영어 | ✅ |
| SUM-007~010 | 고급 요약 | max_length/Gemini/bullet | ✅ |

### 5.5 System & WebSocket - 33개 (23 Pass, 10 Skip)

| TC-ID | 테스트명 | 상태 |
|-------|---------|------|
| SYS-001~016 | 시스템 API | ✅ 16 Pass |
| WS-001~010 | 메시지 형식 검증 | ✅ 7 Pass |
| WS-011~017 | 실제 WS 연결 | ⏭️ 10 Skip |

---

## 6. Frontend 테스트 케이스

### 6.1 Auth Validation - 26개 ✅

| TC-ID | 테스트명 | 설명 | 상태 |
|-------|---------|------|------|
| FE-AUTH-001~004 | 이메일 검증 | 유효/무효/필수/한글 | ✅ |
| FE-AUTH-005~011 | 비밀번호 검증 | 길이/대문자/소문자/숫자/특수문자 | ✅ |
| FE-AUTH-012~014 | 비밀번호 일치 | 일치/불일치/공백 | ✅ |
| FE-AUTH-015~018 | 닉네임 검증 | 공백/길이/허용문자 | ✅ |
| FE-AUTH-019~026 | 추가 검증 | 세션/토큰/에러메시지 | ✅ |

### 6.2 Posts/Comments Validation - 46개 ✅

| TC-ID | 테스트명 | 상태 |
|-------|---------|------|
| FE-POST-001~024 | 게시글 유효성/응답/좋아요/조회수 | ✅ 24 Pass |
| FE-CMT-001~022 | 댓글 유효성/감정분석/권한 | ✅ 22 Pass |

### 6.3 API Structure - 28개 ✅

| TC-ID | 테스트명 | 상태 |
|-------|---------|------|
| FE-API-001~008 | 엔드포인트 URL 형식 | ✅ |
| FE-API-009~020 | 요청/응답 스키마 | ✅ |
| FE-API-021~028 | 에러 핸들링 | ✅ |

---

## 7. 테스트 실행 방법

### 7.1 환경 설정
```bash
# Conda 환경 활성화
source ~/miniconda3/etc/profile.d/conda.sh
conda activate env_python310
```

### 7.2 개별 서비스 테스트
```bash
# Backend 테스트 (80개)
cd FASTAPI_Project_back && python -m pytest -v

# Model 테스트 (83개)
cd FASTAPI_Project_model && python -m pytest -v

# Frontend 테스트 (100개)
cd FASTAPI_Project_front && python -m pytest -v
```

### 7.3 전체 테스트 실행
```bash
# 커버리지 포함
python -m pytest --cov=app --cov-report=html -v
```

---

## 8. 상세 문서 링크

### 📋 테스트 문서 (v4 최신본)

| 문서 | 설명 | 파일 |
|------|------|------|
| **Index** | 전체 테스트 개요 | [TEST_CASES_v4_index.html](./TEST_CASES_v4_index.html) |
| **Backend** | 백엔드 API 테스트 상세 (80개) | [TEST_CASES_v4_backend.html](./TEST_CASES_v4_backend.html) |
| **Model** | AI 모델 테스트 상세 (83개) | [TEST_CASES_v4_model.html](./TEST_CASES_v4_model.html) |
| **Frontend** | 프론트엔드 테스트 상세 (100개) | [TEST_CASES_v4_frontend.html](./TEST_CASES_v4_frontend.html) |
| **Manual** | 수동 테스트 시나리오 (CURL/Postman) | [TEST_CASES_v4_manual.html](./TEST_CASES_v4_manual.html) |

---

## 9. 스킵된 테스트 해결 방법

| 서비스 | 분류 | 스킵 수 | 원인 | 해결 방법 |
|--------|------|---------|------|-----------|
| Model | Ollama Chat | 8개 | Ollama 서비스 미실행 | `ollama serve` 실행 후 테스트 |
| Model | Chat Edge Cases | 4개 | Ollama 서비스 미실행 | `ollama serve` 실행 후 테스트 |
| Model | WebSocket | 6개 | WebSocket 연결 필요 | 통합 환경에서 테스트 |

---

**문서 버전**: v4.0.0  
**최종 수정**: 2025-12-06  
**작성자**: yoon-dong-gyu
