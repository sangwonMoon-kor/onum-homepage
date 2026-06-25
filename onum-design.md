# 온음(ONUM) 디자인 시스템 — DESIGN.md

> 단일 소스(single source of truth). 색·타이포·간격·radius·shadow·라이트/다크 토큰을
> 사람과 AI가 함께 읽는 명세서. 모든 페이지는 이 토큰만 사용한다.
> 구현체: `onum-tokens.js`(Tailwind config) + `onum-base.css`(CSS 변수·유틸).
> getdesign.md 규율을 따른다 — "값을 토큰으로 코드화하면 일관성이 곧 견고함·프리미엄이 된다".

방향: **A — 웜 에디토리얼 강화.** 딥그린·크림 스파인 유지, 토큰·여백·타이포를 단단하게.
차용: Mastercard(웜 크림 편집형) + Apple(여백 절제). 근거: designer_brand_creator persona 팩의
최다 신호 = **ConsistencyLevel → PremiumPositioning / UserExperience / BrandMoat**.

---

## 0. 이 작업이 고치는 "견고함을 깨던" 실제 문제 (검증됨)

| # | 문제 | 해결 |
|---|---|---|
| 1 | `text-headline-sm`이 카드 제목 6곳에 쓰였으나 토큰 미정의 → 크기 무효 | `headline-sm`(24px) 토큰 추가 |
| 2 | 내비/푸터의 `px-lg·px-xl·py-xl·mt-xl·gap-md`가 spacing 토큰에 없음 → 패딩 무효 | 정의된 `margin-*`·`stack-*` 토큰으로 교체 |
| 3 | `max-w-container-max`가 spacing에만 있고 maxWidth에 없음 → 폭 제한 무효 | `maxWidth.container-max` 추가 |
| 4 | Material Symbols `<link>` 중복 로드 | head에서 1회로 정리 |
| 5 | 두 페이지가 토큰 config를 각자 중복 정의 → 드리프트 | `onum-tokens.js` 한 벌을 공유 |
| 6 | 다크 팔레트 미완(`darkMode:"class"`만 존재) | 라이트/다크 색 토큰 완비 |
| 7 | 가짜 통계(수강생 5,000+ 등, "2024년 1월 기준") | 정직성 수정 — 별도 결정(아래 §7) |

---

## 1. 색 토큰

값은 `onum-base.css`에 `R G B` 트리플(CSS 변수)로 정의하고, `onum-tokens.js`가
`rgb(var(--color-x) / <alpha-value>)`로 참조한다 → 알파 조절 가능 + `.dark` 토글로 테마 전환.

| 토큰 | Light | Dark | 용도 |
|---|---|---|---|
| `primary` | `#004639` | `#93d3c0` | 핵심 강조·주요 CTA |
| `primary-container` | `#1b5e4f` | `#055142` | hover·강조 면 |
| `on-primary` | `#ffffff` | `#00382c` | primary 위 텍스트 |
| `on-primary-container` | `#95d5c2` | `#aff0dc` | container 위 텍스트 |
| `secondary` | `#7d562d` | `#f0bd8b` | 웜 보조(앰버/브라운) |
| `secondary-container` | `#ffca98` | `#623f18` | 보조 강조 면 |
| `tertiary` | `#612e23` | `#ffb4a5` | 절제된 포인트(거의 안 씀) |
| `background` / `surface` | `#fbf9f3` | `#12130f` | 페이지 바탕(크림) |
| `surface-container-lowest` | `#ffffff` | `#0b0c09` | 카드 최상 면 |
| `surface-container-low` | `#f5f3ee` | `#1a1c17` | 섹션 교차 배경 |
| `surface-container` | `#f0eee8` | `#1f201b` | 카드 면 |
| `surface-container-high` | `#eae8e2` | `#2a2b25` | 입력·강조 면 |
| `surface-container-highest` | `#e4e2dd` | `#353630` | 이미지 placeholder |
| `on-surface` | `#1b1c19` | `#e4e2dd` | 본문 텍스트 |
| `on-surface-variant` | `#3f4945` | `#c3cbc5` | 보조 텍스트 |
| `outline` | `#707975` | `#8c958f` | 보더(강) |
| `outline-variant` | `#bfc9c4` | `#424a45` | 보더(약·구분선) |
| `error` / `error-container` / `on-error` | `#ba1a1a` / `#ffdad6` / `#fff` | `#ffb4ab` / `#93000a` / `#690005` | 오류 |

**색 사용 규율(절제):** primary green은 강조·CTA·아이콘에만. 본문은 `on-surface`,
보조 본문은 `on-surface-variant`. 배경 깊이감은 `surface-container-*` 단계로만 표현.
면 위 텍스트는 같은 계열의 가장 어두운/밝은 단계로(검정·회색 직접 사용 금지).

---

## 2. 타이포그래피

폰트: **Playfair Display** = display·heading(영문 디스플레이/숫자 감성), **Noto Sans KR** = title·body·label.
한글 본문은 가독성 위해 line-height 넉넉히. 한 화면에 weight는 2~3개로 절제.

| 토큰 | 크기 | line-height | weight | 폰트 | 용도 |
|---|---|---|---|---|---|
| `display-lg` | 64px | 1.1 | 700 | Playfair | 히어로(데스크톱) |
| `display-sm` | 40px | 1.15 | 700 | Playfair | 히어로(모바일) |
| `headline-lg` | 48px | 1.2 | 700 | Playfair | 섹션 대제목 |
| `headline-md` | 32px | 1.3 | 600 | Playfair | 섹션 제목 |
| `headline-sm` | 24px | 1.35 | 600 | Playfair | **카드 제목(신규)** |
| `title-lg` | 20px | 1.4 | 600 | Noto Sans KR | 소제목·강조 |
| `body-lg` | 18px | 1.7 | 400 | Noto Sans KR | 리드 문단 |
| `body-md` | 16px | 1.6 | 400 | Noto Sans KR | 본문 |
| `label-sm` | 12px | 1.2 (자간 0.05em) | 600 | Noto Sans KR | 라벨·메뉴(대문자) |

폰트 패밀리 클래스: `font-display`, `font-heading`, `font-body`.

---

## 3. 간격 — 8px 리듬

| 토큰 | 값 | 용도 |
|---|---|---|
| `stack-sm` | 8px | 요소 내부 |
| `stack-md` | 16px | 요소 간 |
| `stack-lg` | 32px | 블록 간 |
| `stack-xl` | 48px | 큰 블록 간 |
| `gutter` | 24px | 그리드 간격 |
| `section-gap` | 80px | 섹션 세로 리듬 |
| `margin-mobile` | 20px | 모바일 좌우 여백 |
| `margin-desktop` | 64px | 데스크톱 좌우 여백 |

`maxWidth.container-max` = `1280px` (콘텐츠 폭 상한). **`lg/xl/md` 같은 미정의 spacing 클래스 금지.**

---

## 4. radius / shadow

- radius: `DEFAULT` .25rem · `md` .5rem · `lg` .75rem · `xl` 1rem · `full` 9999px. 카드=`lg`, 버튼=`md|lg`, 칩=`full`.
- shadow(green-tinted, 브랜드감): `.soft-shadow` = `0 8px 30px rgb(primary/0.08)` · `.soft-shadow-lg` = `0 16px 48px rgb(primary/0.12)`. 그 외 그림자 금지.
- `.glass-nav` = blur(12px) + `surface/0.8`.

---

## 5. 페이지에서의 사용법

```html
<head>
  <script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
  <script src="onum-tokens.js"></script>            <!-- CDN 다음, 본문 전 (순서 중요) -->
  <link rel="stylesheet" href="onum-base.css" />
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&display=swap" rel="stylesheet" />
  <link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:wght,FILL@100..700,0..1&display=swap" rel="stylesheet" />  <!-- 1회만 -->
</head>
```

다크 모드: `<html class="dark">` 토글. 모든 색이 자동 전환된다.

---

## 6. 파일 구조

```
onum-stitch-from-lazyweb/
├─ onum-design.md            ← 이 문서(명세·근거·변경이력)
├─ onum-tokens.js            ← Tailwind config 1벌(공유)
├─ onum-base.css             ← CSS 변수(라이트/다크) + 공통 유틸
├─ A-home-research.html      ← 홈(토큰 적용·버그 수정)
└─ B-certification-research.html ← 자격증(토큰 적용·버그 수정)
```
`onum-stitch-samples/` 5종은 A안 확정으로 superseded → `_archive/`로 이동(선택).

---

## 7. 미결정 — 통계 섹션(정직성)

현재 홈의 "수강생 5,000+ / 학교 320+ / 자격증 1,200+ / 평점 4.8 (2024년 1월 기준)"은
근거 없는 수치 → 신뢰·정직성 리스크. **실제 숫자 / 신뢰요소 교체 / 제거 중 사용자 결정 대기.**
