<h1 align="center">Push Langdig</h1>

<p align="center">
  <strong>알림으로 배우는 영어 — 한국어 퍼스트 영어 학습 서비스의 원페이지 랜딩</strong>
</p>

<p align="center">
  순수 정적 HTML · Tailwind CSS v4 (CDN) · HTMX · Cloudflare Pages
</p>

---

**Push Langdig**는 영어를 모르는 사람을 위한 한국어 퍼스트 영어 학습 서비스의 랜딩 페이지다. `index.html` 한 파일로 구성된 정적 사이트 — 서버도 빌드 도구도 없고, `main`에 push하면 Cloudflare Pages가 자동 배포한다.

## 설계 포인트

- **빌드 없는 스택** — Tailwind v4를 `@tailwindcss/browser` CDN으로, 테마 토큰은 인라인 `@theme`로 선언
- **점진적 향상** — HTMX가 `#download`의 "스타터 팩 받기" 클릭을 가로채 `fragments/download-ok.html`로 확인 메시지를 스왑. JS가 꺼져 있으면 `<a download>` 폴백으로 파일이 그대로 저장
- **실제 다운로드** — `assets/push-langdig-starter.zip`(표현 카드 30장 CSV + 시작 가이드) 제공
- **앵커 내비** — `#features`, `#how`, `#privacy`, `#download` 단일 페이지 스크롤, 별도 라우트 없음
- **폰트** — Pretendard Variable, JetBrains Mono (CDN)

## 구조

```
index.html                      원페이지 랜딩 (전체 마크업 + @theme 토큰)
fragments/download-ok.html      HTMX 스왑용 다운로드 확인 프래그먼트
assets/push-langdig-starter.zip 스타터 팩 (카드 CSV + 가이드)
assets/cards.csv                표현 카드 소스
assets/starter-guide.md         시작 가이드 소스
DESIGN.md                       디자인 결정 사항
```

## Run

```bash
python3 -m http.server 4173
# open http://localhost:4173
```

## Smoke test

```bash
python3 -m http.server 4173 &
curl -sf http://localhost:4173/ | grep -q 'Push Langdig' && echo OK-index
curl -sf http://localhost:4173/fragments/download-ok.html | grep -q '다운로드가 시작되었습니다' && echo OK-fragment
curl -sfI http://localhost:4173/assets/push-langdig-starter.zip | grep -q '200' && echo OK-zip
```

## Deploy

`main` 브랜치 push → Cloudflare Pages 자동 배포. 별도 빌드 명령 없음.
