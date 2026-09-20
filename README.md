<h1 align="center">Push</h1>

<p align="center">
  <strong>근거 기반 커리어 작업공간 — 채용 공고를 넣으면 이력서·포트폴리오·자기소개서까지 단계별 게이트를 거쳐 만들어주는 AI 워크플로</strong>
</p>

<p align="center">
  랜딩: 순수 정적 사이트 · HTMX · Tailwind CSS v4 · Pretendard
</p>

---

**push-langdig**는 Push의 랜딩 사이트다. Push는 이력서를 "한 번에 생성"하지 않는다. 커리어 근거(이력서, GitHub, 프로젝트 기록)를 수집하고, 채용 공고를 분석하고, Fit score와 작성 전략을 세운 뒤, 단계마다 사람의 승인을 거쳐 최종 문서까지 만든다. AI가 만든 문장은 전부 사용자가 올린 근거에서 나온다. 제품 본체는 [push-fe](https://github.com/push-dot/push-fe)(Tauri 데스크톱 + 웹)와 [push-be](https://github.com/push-dot/push-be)(FastAPI + LangGraph)에 있다.

## 왜 Push인가

| 문제 | 기존 방식 | Push |
| --- | --- | --- |
| AI 이력서가 과장되거나 지어냄 | 프롬프트 한 번에 완성본 요청 | 근거를 검색해 주입, 없는 경험은 쓰지 않음 |
| 결과를 믿을 수 없음 | 결과만 보여줌 | 단계별 게이트 — 각 단계를 보고 진행/수정 결정 |
| 공고마다 따로 관리 | 스프레드시트 수작업 | 공고 URL을 붙여넣으면 지원 항목이 자동 생성·연결 |
| 문서가 채팅에 묻힘 | 복사해서 별도 편집 | 생성물이 `내 서류` 문서로 동기화, PDF/DOCX로 보내기 |

## 주요 기능

- **단계별 워크플로** — 근거 파싱 → 공고 분석 → Fit score → 전략 → 초안 → 품질 검증 → PDF. 각 단계는 사용자 승인을 거친다
- **근거 수집** — 이력서 업로드, GitHub 리포 탐색, 채용 공고 URL fetch
- **끊기지 않는 스트림** — 페이지를 나갔다 와도 진행 중 생성이 자동 재연결
- **역할별 모델 라우팅** — 관리형 모델과 BYOK 모두 지원
- **문서화** — 생성물을 문서로 자동 동기화, 에디터로 다듬고 PDF/DOCX로 보내기
- **지원 관리·면접 준비·프로젝트 기획서** — 이력서 외 산출물도 같은 근거에서 생성

## 스택

- **정적 원페이지** — `index.html` 단일 파일, 백엔드·빌드 도구 없음
- **Tailwind CSS v4** — `@tailwindcss/browser` CDN + 인라인 `@theme` 토큰
- **HTMX 2.x** — 다운로드 확인 프래그먼트(`fragments/download-ok.html`) 스왑
- **Pretendard Variable + JetBrains Mono** — CDN 폰트
- 디자인 토큰·레이아웃 규칙·수용 부채는 [DESIGN.md](DESIGN.md) 참조

## 시작하기

```sh
python3 -m http.server 4173
# http://localhost:4173
```

## 다운로드 동작

"스타터 팩 받기" 버튼은 실제 파일 `assets/push-starter.zip`(이력서 점검 체크리스트 + 공고 분석 템플릿)을 저장한다.

- JS 있음 — HTMX가 `fragments/download-ok.html`을 가져와 `#download-status`에 확인 메시지를 스왑하고, 같은 클릭으로 ZIP 다운로드 실행
- JS 없음 — `<a download>` 폴백으로 파일이 그대로 저장

## 스모크 테스트

```sh
python3 -m http.server 4173 &
curl -sf http://localhost:4173/ | grep -q '커리어 작업공간' && echo OK-index
curl -sf http://localhost:4173/fragments/download-ok.html | grep -q '다운로드가 시작되었습니다' && echo OK-fragment
curl -sfI http://localhost:4173/assets/push-starter.zip | grep -q '200' && echo OK-zip
```

## 구조

```
index.html                       원페이지 랜딩 (앵커 내비: #features #how #privacy #download)
fragments/download-ok.html       HTMX 다운로드 확인 프래그먼트
assets/push-starter.zip          다운로드 아티팩트
assets/career-checklist.md       스타터 팩 안내 (ZIP 원본)
assets/resume-checklist.md       이력서 점검 체크리스트 (ZIP 원본)
assets/job-analysis-template.md  공고 분석 템플릿 (ZIP 원본)
DESIGN.md                        디자인 리서치·토큰·규칙·수용 부채
```
