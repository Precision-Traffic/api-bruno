# Solid Connection API - Bruno Collection

이 레포지토리는 Solid Connection 서비스의 API 명세를 [Bruno](https://www.usebruno.com/) 형식으로 관리하는 프로젝트입니다.

## 프로젝트 개요

[bruno-api-typescript](https://github.com/manNomi/bruno-api-typescript)를 사용하여 Bruno API 컬렉션을 TypeScript 타입과 React Query 훅으로 자동 변환합니다.

## 디렉토리 구조

```
api-bruno/
├── auth/                       # 인증 관련 API (회원가입, 로그인, 소셜 로그인 등)
├── universities/               # 대학교 관련 API
│   └── univ-apply-infos/      # 대학 지원 정보
├── mypage/                     # 마이페이지 API
├── applications/               # 지원 정보 API
├── community/                  # 커뮤니티 API
│   ├── boards/                # 게시판
│   ├── posts/                 # 게시글
│   └── comments/              # 댓글
├── grades/                     # 성적 등록 API
├── admin/                      # 어드민 API
├── users/                      # 사용자 관리 API
├── mentors/                    # 멘토 관련 API
│   ├── mentor/                # 멘토 정보
│   ├── mentor-only/           # 멘토 전용 기능
│   └── mentee/                # 멘티 전용 기능
├── newsletters/                # 소식지 API
├── reports/                    # 신고 API
├── chat/                       # 채팅 API
├── image-upload/               # 이미지 업로드 API
├── kakao/                      # 카카오 API
├── environments/               # 환경 변수 설정
│   ├── local.bru              # 로컬 환경
│   └── dev.bru                # 개발 환경
├── bruno.json                  # Bruno 컬렉션 설정
└── collection.bru              # 컬렉션 메타데이터
```

## 주요 기능

### 1. 인증 (auth/)
- 회원가입 / 이메일 로그인
- 카카오 / 애플 소셜 로그인
- 토큰 재발급 / 로그아웃
- 회원 탈퇴

### 2. 대학교 관련 (universities/)
- 대학 검색 (텍스트, 필터)
- 학교 상세 정보 조회
- 사용자 맞춤 대학 추천
- 위시리스트 관리

### 3. 커뮤니티 (community/)
- 게시판 / 게시글 / 댓글 CRUD
- 좋아요 기능

### 4. 멘토링 (mentors/)
- 멘토 목록 조회 및 상세 정보
- 멘토링 신청 / 수락 / 거절
- 매칭된 멘토 관리

### 5. 지원 정보 (applications/)
- 지원서 제출
- 지원자 현황 조회
- 경쟁률 확인

### 6. 성적 관리 (grades/)
- 학점 / 어학 성적 등록 및 조회

### 7. 어드민 (admin/)
- 학점 / 어학 성적 검증

## 사용 방법

### 1. Bruno 앱에서 열기

1. [Bruno 다운로드](https://www.usebruno.com/downloads)
2. Bruno 앱 실행
3. "Open Collection" 클릭
4. 이 레포지토리의 루트 디렉토리 선택

### 2. bruno-api-typescript로 타입 생성

```bash
# OpenAPI 스펙 생성
npx bruno-api-typescript generate -i ./api-bruno -o ./openapi.json

# React Query 훅 생성
npx bruno-api-typescript generate-hooks -i ./api-bruno -o ./src/apis
```

### 3. 환경 변수 설정

`environments/` 폴더에서 환경별로 설정:
- `local.bru`: 로컬 개발 환경 (http://localhost:3000/api)
- `dev.bru`: 개발 서버 환경

## API 명세 작성 가이드

### .bru 파일 형식

```bru
meta {
  name: API 이름
  type: http
  seq: 1
}

post {
  url: {{baseUrl}}/endpoint
  body: json
  auth: bearer
}

auth:bearer {
  token: {{token}}
}

body:json {
  {
    "key": "value"
  }
}

docs {
  ```json
  {
    "response": "example"
  }
  ```
}
```

### docs 블록 작성 규칙

**중요**: `docs` 블록의 JSON이 TypeScript 타입 생성의 기준이 됩니다.

1. 모든 필드를 포함 (옵셔널 포함)
2. 정확한 타입 표기:
   - 문자열: `"hello"`
   - 숫자: `123` 또는 `4.5`
   - 불린: `true` / `false`
   - 배열: `[1, 2, 3]` (최소 1개 요소)
   - 날짜: ISO 8601 형식 (`"2025-11-14T00:00:00Z"`)

## 통계

- 총 API 엔드포인트: **98개**
- 도메인 카테고리: **13개**

## 관련 링크

- [bruno-api-typescript](https://github.com/manNomi/bruno-api-typescript)
- [Bruno 가이드](https://github.com/manNomi/bruno-api-typescript/blob/main/docs/bruno-guide.md)
- [Bruno 공식 사이트](https://www.usebruno.com/)

## 라이선스

MIT
