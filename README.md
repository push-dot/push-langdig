# push-langdig

밀어넣는 영어, 파고드는 학습. 한국어 사용자를 위한 영어 학습 도구의 원페이지 랜딩 사이트입니다.

## 구조

```
index.html                     원페이지 랜딩 (Tailwind CDN + HTMX CDN)
fragments/download-ok.html     HTMX로 로드되는 다운로드 확인 프래그먼트
assets/push-langdig-starter.zip 시작 가이드 + 30일 어휘 CSV
DESIGN.md                      디자인 토큰과 구조 설명
```

## 로컬 실행

```bash
python3 -m http.server 4173
# http://localhost:4173
```

## 특징

- 단일 페이지, 스크롤 앵커 네비게이션 (`#features`, `#flow`, `#privacy`, `#download`)
- 스티키 내비게이션 + 모바일 메뉴
- HTMX 점진적 향상: 다운로드 확인 메시지를 프래그먼트로 로드
- 실제 동작하는 zip 다운로드 링크
- 의존성 없음 — 정적 CDN만 사용
- `prefers-reduced-motion`, 포커스 링, `aria-live` 지원
