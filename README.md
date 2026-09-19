# push-langdig

Push 데스크톱 앱의 랜딩 페이지. https://push-langdig.pages.dev

## 구조

```
index.html                     원페이지 랜딩 (순수 HTML/CSS/JS)
fragments/                     페이지 프래그먼트
DESIGN.md                      디자인 토큰과 구조 설명
```

## 로컬 실행

```bash
python3 -m http.server 4173
# http://localhost:4173
```

## 배포

- Cloudflare Pages, Git 연동 — `main` 브랜치 푸시 시 프로덕션 자동 배포
- `develop` 등 다른 브랜치는 프리뷰 배포
- 작업은 `develop`에서, 머지 대상은 `main`

## 다운로드 링크

GitHub Releases `latest` 고정 링크 — push-fe에 `v*` 태그가 푸시되면 CI가 새 설치 파일을 올리고 랜딩은 자동으로 최신을 가리킨다.

- macOS: `https://github.com/push-dot/push-fe/releases/latest/download/Push_aarch64.dmg`
- Windows: `https://github.com/push-dot/push-fe/releases/latest/download/Push_x64-setup.exe`

macOS는 서명/공증이 없어 Gatekeeper 경고가 뜬다. 랜딩의 다운로드 버튼이
`xattr -cr /Applications/Push.app` 안내 모달을 띄운다.
