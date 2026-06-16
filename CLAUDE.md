# CLAUDE.md

이 파일은 이 저장소에서 코드 작업을 할 때 Claude Code(claude.ai/code)에 대한 지침을 제공합니다.

## 프로젝트 개요

Vanilla HTML, CSS, JavaScript로 만든 개발자 웹 이력서 & 포트폴리오 사이트입니다. TailwindCSS CDN을 사용하므로 빌드 도구나 복잡한 의존성이 없습니다.

## 아키텍처

**단일 페이지 구조** 로 다음 섹션들로 구성:
- 네비게이션 (고정 헤더 + 모바일 햄버거 메뉴)
- Hero 섹션 (소개)
- About, Experience, Projects, Skills, Contact 섹션
- 푸터

**기술 스택:**
- **HTML5**: `index.html` 에 TailwindCSS 유틸리티 클래스를 활용한 시맨틱 마크업
- **CSS**: `css/style.css` 에 커스텀 애니메이션, 트랜지션, 미디어 쿼리 정의
- **JavaScript**: `js/main.js` 에서 모바일 메뉴 토글, 부드러운 스크롤, 네비게이션 활성화, 폼 제출 처리

**스타일 방식:**
- TailwindCSS CDN 로드 (PostCSS/purge 불필요)
- 커스텀 애니메이션은 `css/style.css` 에 정의
- 반응형 클래스 (sm/md/lg 브레이크포인트) 를 HTML에 인라인으로 작성

## 개발

### 로컬 서버 실행 (권장)

Python 내장 HTTP 서버로 로컬 테스트:
```bash
python3 -m http.server 8000
# 또는
python -m SimpleHTTPServer 8000
```

브라우저에서 `http://localhost:8000` 접속. 상대 경로가 올바르게 작동하고 부드러운 스크롤이 작동합니다.

또는 `index.html` 을 브라우저에서 직접 열어도 되지만, 서버 실행이 더 안정적입니다.

### 파일 편집

**콘텐츠 수정:**
- 모든 이력서/포트폴리오 콘텐츠는 `index.html` 에 위치 (이름, 자기소개, 경력, 프로젝트, 기술, 연락처)
- HTML에서 직접 텍스트 편집 (각 섹션은 명확한 id 속성이 있음)

**스타일 수정:**
- HTML 속성의 TailwindCSS 클래스로 전역/반응형 스타일 적용
- 커스텀 애니메이션/트랜지션은 `css/style.css` 에 정의
- 새 섹션 추가 시 기존 패딩/간격 패턴 따르기 (예: `mb-20`, `py-6`)

**JavaScript:**
- 모바일 메뉴 토글, 부드러운 스크롤, 네비게이션 활성화 상태, 폼 제출 처리
- 외부 라이브러리 없이 Vanilla JS 사용
- 스크립트 태그 순서에 따라 이벤트 핸들러가 자동 연결됨

## 배포

### GitHub Pages (권장)
1. `username.github.io` 이름으로 저장소 생성
2. 프로젝트 파일을 main 브랜치에 푸시
3. 자동으로 `https://username.github.io` 에 배포됨

### Netlify / Vercel
- 프로젝트 폴더를 드래그&드롭하면 즉시 배포
- 별도의 빌드 단계 불필요

### 배포 전 로컬 테스트
- 모바일에서 테스트 (Chrome DevTools 반응형 모드)
- 모든 링크와 폼 제출 확인
- TailwindCSS 클래스가 렌더링되는지 확인 (CDN으로 로드됨)

## 주요 패턴

**모바일 반응형:**
- 네비게이션은 모바일에서 숨김, 햄버거 메뉴로 표시
- 그리드 레이아웃: `grid-cols-1 md:grid-cols-2` (모바일은 1열, 태블릿 이상은 2열)
- 패딩/텍스트 크기는 `css/style.css` 의 미디어 쿼리로 조정

**인터랙션:**
- 부드러운 스크롤: 앵커 클릭 시 기본 동작 방지, `scrollIntoView({ behavior: 'smooth' })` 사용
- 활성 네비게이션: 스크롤 시 계산, 해당 섹션 ID와 일치하면 클래스 업데이트
- 폼 제출: 기본 동작 방지, 알림 표시, 입력 필드 초기화

## 일반적인 작업

| 작업 | 수행 방법 |
|------|---------|
| 이력서 콘텐츠 수정 | `index.html` 섹션 텍스트 편집 (About, Experience, Projects, Skills, Contact) |
| 색상/테마 변경 | HTML의 TailwindCSS 클래스 수정 또는 `css/style.css` 의 그래디언트/색상 값 조정 |
| 새 프로젝트 추가 | `index.html` 에서 프로젝트 카드 div 복사 후 내용 수정 |
| 모바일 레이아웃 수정 | Chrome DevTools 반응형 모드에서 테스트, 그리드/패딩 클래스 또는 `css/style.css` 미디어 쿼리 조정 |
| 웹에 배포 | GitHub Pages에 푸시 또는 Netlify/Vercel에 폴더 드래그 |
| 로컬 테스트 | `python3 -m http.server 8000` 실행 후 `http://localhost:8000` 접속 |

## 주의사항

- TailwindCSS는 CDN으로 로드됨—npm/빌드 단계 불필요하지만, 프로젝트 성장 시 파일 크기와 커스터마이징 고려 필요
- API 통합 없음; 연락처 폼은 클라이언트 전용 (알림만 표시, 백엔드 없이는 이메일 미전송)
- 모바일 메뉴는 Vanilla JS 토글 사용, 프레임워크 없음
- 모든 경로는 상대 경로이므로 로컬/모든 웹 서버에서 작동

---

**마지막 업데이트:** 2026-06-15
