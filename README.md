<h1 align="center">Push Langdig</h1>

<p align="center">
  <strong>맥락으로 배우는 영어 — 앱을 열지 않아도 알림이 수업이 되는, 영어를 모르는 사람을 위한 한국어 퍼스트 학습</strong>
</p>

<p align="center">
  순수 정적 사이트 · HTMX · Tailwind CSS v4 · Pretendard
</p>

---

**push-langdig**는 Push Langdig의 랜딩 사이트다. Push Langdig는 영어를 모르는 사람이 맥락 속에서 표현을 익히는 학습 앱이다. 하루 몇 번 짧은 영어 카드를 알림으로 보내고, 영어 설명 대신 한국어로만 설명하며, 계정 없이 기기 안에서만 기록을 남긴다.

## 왜 Langdig인가

| 문제 | 기존 방식 | Langdig |
| --- | --- | --- |
| 앱을 여는 것부터가 진입 장벽 | 앱 실행 → 레벨 테스트 → 커리큘럼 | 잠금 화면의 알림 한 장이 곧 수업 |
| 영어 설명을 읽으려면 영어가 필요 | 영어로 된 UI와 해설 | 모든 카드와 설정이 한국어 |
| 문법 위주라 생활에서 안 쓰임 | 교과서 문장 암기 | 카페·지하철·회의에서 실제로 쓰는 표현만 |
| 가입과 추적이 부담 | 이메일 가입, 광고 SDK | 로그인 없음, 기기 로컬 저장, 삭제하면 끝 |

## 주요 기능

- **알림이 곧 수업** — 아침·점심·저녁, 잠금 화면에 뜨는 카드 한 장. 읽는 데 10초
- **한국어 퍼스트** — 영어를 몰라도 바로 시작. 모든 설명은 한국어
- **자동 재노출** — "모르겠어요"를 누른 표현은 며칠 뒤 다시 알림으로 온다
- **생활 표현 큐레이션** — 주문·길 안내·전화·거절처럼 상황별로 고른 실전 문장
- **프라이버시** — 계정 없음, 학습 기록은 기기에만 저장, 광고 추적 없음

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

"스타터 팩 받기" 버튼은 실제 파일 `assets/push-langdig-starter.zip`(표현 카드 30장 CSV + 시작 가이드)을 저장한다.

- JS 있음 — HTMX가 `fragments/download-ok.html`을 가져와 `#download-status`에 확인 메시지를 스왑하고, 같은 클릭으로 ZIP 다운로드 실행
- JS 없음 — `<a download>` 폴백으로 파일이 그대로 저장

## 스모크 테스트

```sh
python3 -m http.server 4173 &
curl -sf http://localhost:4173/ | grep -q 'Push Langdig' && echo OK-index
curl -sf http://localhost:4173/fragments/download-ok.html | grep -q '다운로드가 시작되었습니다' && echo OK-fragment
curl -sfI http://localhost:4173/assets/push-langdig-starter.zip | grep -q '200' && echo OK-zip
```

## 구조

```
index.html                     원페이지 랜딩 (앵커 내비: #features #how #privacy #download)
fragments/download-ok.html     HTMX 다운로드 확인 프래그먼트
assets/push-langdig-starter.zip 다운로드 아티팩트
assets/cards.csv               표현 카드 30장 (ZIP 원본)
assets/starter-guide.md        시작 가이드 (ZIP 원본)
DESIGN.md                      디자인 리서치·토큰·규칙·수용 부채
```
