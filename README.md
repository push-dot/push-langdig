# Push Langdig

알림으로 배우는 영어. 영어를 모르는 사람을 위한 한국어 퍼스트 영어 학습 서비스의 원페이지 랜딩.

## Stack

- 순수 정적 사이트: `index.html` 한 페이지, 서버/빌드 도구 없음
- Tailwind CSS v4 (`@tailwindcss/browser` CDN) + 인라인 `@theme` 토큰
- HTMX 2.x: 다운로드 확인 프래그먼트(`fragments/download-ok.html`) 스왑
- 폰트: Pretendard Variable, JetBrains Mono (CDN)

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

## Download behavior

`#download`의 "스타터 팩 받기" 버튼은 실제 파일 `assets/push-langdig-starter.zip`(표현 카드 30장 CSV + 시작 가이드)을 내려받습니다.

- JS 있음: HTMX가 `fragments/download-ok.html`을 가져와 `#download-status`에 확인 메시지를 스왑하고, 동일 클릭으로 ZIP 다운로드를 트리거합니다.
- JS 없음: `<a download>` 폴백으로 파일이 그대로 저장됩니다.

## Nav

모든 내비게이션은 동일 페이지 앵커(`#features`, `#how`, `#privacy`, `#download`)로 스크롤합니다. 별도 라우트 없음.
