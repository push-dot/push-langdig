# push-langdig 디자인 노트

## 비주얼 토큰

| 토큰 | 값 | 용도 |
| --- | --- | --- |
| ink | `#090b0c` | 기본 배경, 다크 섹션 |
| inkSoft | `#14181b` | 카드/칩 배경 |
| surface | `#f5f5f5` | 라이트 섹션 배경, 텍스트 |
| accent | `#00a5ef` | 주요 액센트, CTA |
| accentDeep | `#0084cc` | 호버/라이트 섹션 액센트 |
| line | `rgba(245,245,245,0.08)` | 다크 섹션 보더 |
| lineDark | `rgba(9,11,12,0.08)` | 라이트 섹션 보더 |

## 형태

- pill 네비게이션 바 (`rounded-full`, `backdrop-blur`)
- squircle 카드/버튼 (`border-radius: 20px`)
- 배경: 56px 그리드 라인 + 상단 radial glow (`rgba(0,165,239,0.18)`)

## 섹션 구조

1. Hero (`#top`) — 다크, 그리드+glow, 디스플레이 헤드라인, 부유 카드 3장
2. Features (`#features`) — 라이트, 3열 카드
3. Learning Flow (`#flow`) — 다크, 번호 리스트 01–03
4. Privacy (`#privacy`) — 라이트, 2열
5. Download (`#download`) — 다크, CTA + HTMX 상태 영역
6. Footer — 다크, 앵커 링크 반복

다크/라이트 섹션 교차로 에디토리얼 리듬 생성.

## 타이포

- Pretendard → Inter → system fallback
- 헤드라인 `font-extrabold`, `tracking-tight`, 4xl–6xl
- 섹션 라벨: `uppercase tracking-widest` + accent 컬러

## 반응형

- 모바일(390px): 좌측 정렬 히어로, 24px 거터(`px-6`), 햄버거 메뉴
- 데스크톱: 히어로 센터(`lg:text-center`), 섹션 패딩 `py-32`, `max-w-6xl`

## 접근성

- `prefers-reduced-motion` 시 scroll-behavior/애니메이션 무력화
- `:focus-visible` cyan 아웃라인
- 스킵 링크, `aria-expanded`/`aria-controls` 메뉴, `aria-live` 다운로드 상태

## 상호작용

- Tailwind CSS CDN + HTMX CDN만 사용, 빌드 없음
- 다운로드는 네이티브 `<a download>` — 실제 zip 제공
- HTMX `hx-get`이 `fragments/download-ok.html`을 `#download-status`에 삽입
- 모바일 메뉴는 최소 바닐라 JS
