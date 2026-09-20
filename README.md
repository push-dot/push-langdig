<h1 align="center">Push Landing</h1>

<p align="center">
  <strong>근거 기반 커리어 작업공간 Push의 원페이지 랜딩 — 디자인 시스템부터 접근성까지 직접 설계한 정적 사이트</strong>
</p>

<p align="center">
  HTML · Tailwind CSS v4 · HTMX · Pretendard
</p>

---

## 프로젝트 소개

Push 제품(채용 공고를 넣으면 이력서·자기소개서까지 단계별로 만들어주는 AI 커리어 앱)의 랜딩 페이지입니다. 프레임워크 없이 `index.html` 단일 파일로 구현했고, Aside 스타일의 에디토리얼 SaaS 무드를 참고해 오리지널 디자인 토큰과 레이아웃 문법을 정의했습니다.

## 이 프로젝트에서 보여주는 것

- **디자인 시스템 설계** — ink/paper/시안 액센트 토큰, 스쿼클·필 컨트롤, 그리드·노이즈 디테일을 `@theme`으로 선언. 근거는 [DESIGN.md](DESIGN.md)에 문서화
- **프로그레시브 인핸스먼트** — 다운로드 버튼은 JS 없이 `<a download>`로 동작하고, HTMX가 있으면 확인 상태를 `aria-live` 영역에 스왑
- **접근성** — `lang="ko"` 시맨틱 마크업, 스킵 링크, `:focus-visible` 아웃라인, `prefers-reduced-motion` 대응
- **한국어 UX 카피** — 제품의 단계별 게이트 워크플로와 근거 기반 생성을 한 화면의 섹션 구조로 풀어냄
- **실제 다운로드 아티팩트** — 가짜 링크가 아니라 이력서 체크리스트와 공고 분석 템플릿이 담긴 ZIP을 생성해 제공

## 스택

- **정적 원페이지** — 빌드 도구·백엔드 없이 단일 HTML
- **Tailwind CSS v4** — `@tailwindcss/browser` + 인라인 디자인 토큰
- **HTMX 2.x** — 다운로드 확인 프래그먼트 스왑
- **Pretendard Variable + JetBrains Mono**

## 로컬에서 보기

```sh
python3 -m http.server 4173
# http://localhost:4173
```
