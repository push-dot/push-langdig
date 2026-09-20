# DESIGN.md - Push landing

## Reference research

Visual grammar inspired by aside.com (measured live, per brief notes):

- Ink `#090b0c`, pale surface `#f5f5f4`, electric accent `#00a5ef` / `#0084cc`
- Geist-like UI sans + editorial display headline, pill/squircle controls
- Generous whitespace, subtle grid + noise, floating rounded nav
- Mobile ~390px: hamburger nav, left-aligned ~36px hero, 24px gutters
- Desktop: 64-72px nav, max-w-6xl content column

Original identity: "P" squircle mark (ink tile, cyan stroke path), Korean-first copy for the Push career workspace product. No Aside assets, copy, or logo reused.

## Tokens

| Token | Value | Use |
|---|---|---|
| `--color-ink` | `#090b0c` | text, dark panels, primary CTA |
| `--color-paper` | `#f5f5f4` | page surface |
| `--color-accent` | `#00a5ef` | marks, icons, links on dark |
| `--color-accent-deep` | `#0084cc` | mono labels, status text (AA on paper) |
| `--font-sans` | Pretendard Variable | all UI + display (Korean-first) |
| `--font-mono` | JetBrains Mono | small uppercase labels only |

Theme: light, locked. One deliberate dark color-block: privacy section (ink panel). One accent across the whole page.

## Typography

- Display: Pretendard Variable 700, `tracking-tight`, 38-54px, 2-line max hero
- Body: 15-17px, `leading-relaxed`, ink at 55-65% opacity
- Labels: JetBrains Mono 10-11px, `tracking-[0.18-0.22em]`, used sparingly (hero eyebrow, card meta, step verbs)

## Layout grammar

- `max-w-6xl`, gutters 16px mobile / 24px sm+
- Sections: hero (grid-mask bg, left-aligned) → notification card strip → bento features (6-col, 4+2/2+4 rhythm, exact cell count) → 3-col steps → ink privacy panel → centered download CTA → footer
- Corner system: pill for interactive controls, `rounded-[1.75rem]-[2rem]` for panels, `rounded-2xl/3xl` nested cards
- Nav: floating pill, backdrop-blur, `details/summary` hamburger under `md`

## Motion

- MOTION_INTENSITY 3: `scroll-behavior: smooth`, color/scale transitions, `:active` push. No scroll listeners, no loops.
- `prefers-reduced-motion`: smooth scroll off, all transitions/animations disabled.

## Responsive

- <768px: hamburger (`details`), single-column grids, 38px hero, stacked footer
- 768px+: inline nav links, bento/3-col grids, ~54px hero

## Accessibility

- `lang="ko"`, semantic `header/nav/main/section/footer`, skip link, `aria-live` download status, `:focus-visible` accent outline, accent-deep text meets AA on paper, SVG icons `aria-hidden`

## HTMX

- Download CTA: `hx-get` fetches `fragments/download-ok.html` into `#download-status` (aria-live). `hx-on::before-request` programmatically clicks the `download` URL so the same click both saves the ZIP and renders confirmation. Without JS: plain `<a download>` still downloads the file.

## Accepted debt

- Tailwind via `@tailwindcss/browser` CDN (dev-grade JIT; swap for a compiled stylesheet when the project graduates)
- Fonts from CDN, no local self-hosting yet
- No automated visual regression; manual + curl smoke only
