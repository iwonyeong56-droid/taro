---
name: 오늘의 타로
version: 0.2
source: "명지대학교 타로 디자인 팩.fig (2026-11-07 내보냄)"
theme: light
base-style: luma          # shadcn style: 둥근 버튼 · 넉넉한 여백
viewport: mobile-first    # 375 × 812 기준
colors:
  bg: "#f3f3f5"
  surface: "#ffffff"
  surface-sub: "#f6f6f8"
  text-primary: "#000000"
  text-secondary: "#4d4d4e"
  text-tertiary: "#979f9b"
  text-on-accent: "#000000"   # 팩은 #ffffff → 대비 1.90이라 검정으로 바꿈 (§2-3)
  border: "#dcdcdd"
  accent: "#00d959"
  accent-soft: "#e6faef"
  accent-strong: "#00d959"
  accent-illust: "#00de00"
  disabled: "#d7d7d7"
  danger: "#e5484d"
  inverse: "#232427"
typography:
  family: "Noto Sans KR, system-ui, -apple-system, 'Apple SD Gothic Neo', 'Malgun Gothic', sans-serif"
  letter-spacing: -2%
rounded:
  card-front: 10px
  input: 12px
  button-m: 14px
  button-l: 16px
  sheet: 24px
  card: 24px
  pill: 9999px
spacing:
  unit: 4px
  gutter: 20px
  status-bar: 44px
  home-indicator: 34px
components:
  button-l: { fill: accent, text: text-on-accent, radius: 16px, size: 335x56 }
  button-m: { fill: accent | surface, radius: 14px, size: 162x48 }
  topic-chip: { fill: surface, selected-fill: accent-soft, selected-border: accent 1.5px, radius: pill, size: 105x44 }
  input: { fill: surface, border: border, radius: 12px, height: 52px }
  result-card: { fill: surface, radius: 24px, padding: 28px 24px, size: 335x534 }
  tarot-card-front: { radius: 10px, size: 160x268, shadow: card }
  tarot-card-back: { fill: surface, border: accent 2px, radius: 12px, size: 120x200 }
---

# 오늘의 타로 — Design Guide

> **연회색 바탕 위 흰 카드, 초록 강조 하나.** 진짜 타로 그림(라이더-웨이트-스미스 1909)을 주인공으로 두고, 나머지 화면은 조용하고 깔끔하게.

이 문서는 선배가 준 디자인 시스템 파일 **「명지대학교 타로 디자인 팩.fig」**(2026-11-07 내보냄)을 기준으로 다시 쓴 것입니다. 기획 문서(`TARO_01_PRD` ~ `TARO_04_와이어프레임`)와 맞지 않거나 팩에 없는 부분은 사용자 결정(2026-11-19)으로 채웠고, 그런 곳에는 **[결정]** 표시를 붙였습니다.

구현은 **Tailwind CSS v4 + shadcn/ui**를 기준으로 합니다.

### v0.1 → v0.2 바뀐 점

| 항목 | v0.1 (내 첫 가이드) | v0.2 (디자인 팩 기준) |
|---|---|---|
| 분위기 | 종이 스크랩북 콜라주 | 연회색 바탕 + 흰 라운드 카드 + 초록 강조 |
| 바탕 · 강조 | Canvas `#fff3e7` · Ink 버튼 · Papaya 액자 | bg `#f3f3f5` · accent `#00d959` |
| 글꼴 | Gowun Batang(세리프) + Pretendard | **Noto Sans KR 하나**, 자간 -2% |
| 주제 색 | 주제마다 파스텔 6개 | 없음. 선택은 초록 하나로 표시 **[결정: 전부 팩으로 교체]** |
| 카드 그림 | 미정 (임시 선그림) | 라이더-웨이트-스미스 1909 메이저 아르카나 22장 |
| 결과 카드 | 4:5 (1080×1350) | 335×534 → 저장 이미지 **1080×1722** **[결정: 팩 비율]** |
| 카드 뽑기 | 버튼 → 바로 뒤집기 | 22장 부채꼴 덱에서 골라 뒤집기 **[결정: 팩 흐름 넣기]** |
| 장식 | 점 격자 · 종이 조각 | 없음 (카드 그림만) |

## 1. 디자인 방향

| 기획에서 온 요구 | 디자인으로 푸는 방법 |
|---|---|
| 로그인 없이 1분 안에 끝 (PRD 1) | 화면마다 큰 초록 버튼(L)은 하나. 나머지 행동은 흰 버튼. |
| "내 얘기" 같은 해석 (PRD 2) | 결과 카드 맨 위에 "지민님의 타로 · 커리어", 카드 아래에 별자리. 해석 3줄은 가운데 정렬. |
| 개인정보를 남기지 않음 (원칙 1) | 🔒 Privacy Notice를 입력칸 아래 · 결과 버튼 아래에 **같은 모양**으로 고정. |
| 이미지 한 장으로 공유 (F-5 · F-6) | Result Card 영역 = 저장 이미지. |
| 오락용 해석 (원칙 4) | 무서운 어둠 대신 밝은 연회색 · 흰색. "※ 오락용 타로 해석입니다"를 카드 안에 항상. |

**한 줄 원칙:** 바탕은 bg, 담는 건 흰 surface, 행동과 선택은 accent 초록, 글자는 검정.

## 2. 색 (Colors)

팩의 Figma 변수 컬렉션 `Taro`(모드 Light)를 그대로 씁니다. 팩 설명: 레퍼런스(uibowl 타로 화면)에서 실제 픽셀을 뽑은 값.

### 2-1. 토큰

| 토큰 | 값 | 역할 |
|---|---|---|
| `color/bg` | `#F3F3F5` | 모든 화면 바탕 |
| `color/surface` | `#FFFFFF` | 카드 · 입력칸 · 흰 버튼 · 시트 |
| `color/surface-sub` | `#F6F6F8` | Privacy Notice 바탕, 공유 글 상자 |
| `color/text/primary` | `#000000` | 제목 · 본문 · 입력값 |
| `color/text/secondary` | `#4D4D4E` | 설명 · 라벨 · 안내문 · 오락용 안내 |
| `color/text/tertiary` | `#979F9B` | 입력칸 placeholder, 장식용 글자만 (§2-3) |
| `color/text/on-accent` | `#000000` | 초록 버튼 위 글자 **[결정]** (팩 값 `#FFFFFF`) |
| `color/border` | `#DCDCDD` | 테두리 · 구분선 |
| `color/accent` | `#00D959` | 주 버튼 바탕, 선택 테두리, 카드 뒷면 테두리 |
| `color/accent-soft` | `#E6FAEF` | 선택된 주제 칩 바탕, 카드 뒷면 가운데 원 |
| `color/accent-strong` | `#00D959` | (팩에서 accent와 같은 값. 따로 쓰지 않음) |
| `color/accent-illust` | `#00DE00` | 스와이프 안내 그림 · "Swipe!" 글자 (장식) |
| `color/disabled` | `#D7D7D7` | 비활성 버튼 바탕 |
| `color/danger` | `#E5484D` | 입력 오류 테두리 · 오류 문구 |
| `color/inverse` | `#232427` | 토스트 바탕, 시트 뒤 어둡게(55%) |

### 2-2. 대비 (WCAG, 직접 계산)

| 글자 / 바탕 | 대비 | 판정 |
|---|---|---|
| text/primary / bg | 18.95 | ✓ |
| text/secondary / bg · surface · surface-sub | 7.62 · 8.44 · 7.82 | ✓ |
| text/tertiary / bg · surface | 2.45 · 2.71 | ✕ → 글자로 쓰지 않음 |
| **흰 글자 / accent** (팩 원래) | **1.90** | ✕ |
| **검정 글자 / accent** (v0.2) | **11.07** | ✓ |
| accent 글자 / surface | 1.90 | ✕ → 초록 글자 금지 |
| 흰 글자 / disabled (팩 원래) | 1.44 | ✕ |
| text/secondary / disabled (v0.2) | 5.87 | ✓ |
| 흰 글자 / inverse | 15.52 | ✓ |
| danger 글자 / surface | 3.91 | △ (§11 알려진 문제) |

### 2-3. 색을 쓰는 규칙 [결정: 대비 맞추기]

- **초록은 바탕 · 테두리 · 그림에만.** 초록 글자는 쓰지 않습니다. 팩에서 초록 글자였던 곳은 이렇게 바꿉니다.
  - 결과 카드 Meta "XIX 태양 · 사자자리" → text/primary
  - 선택된 주제 칩 글자 → text/primary Bold (바탕 accent-soft + 테두리 accent 1.5px는 그대로)
- **초록 버튼 위 글자는 검정**(`text/on-accent` = `#000000`). 팩에 있는 색만 썼습니다.
- **비활성 버튼 글자는 text/secondary.** 팩은 흰 글자였습니다.
- **tertiary는 placeholder와 장식에만.** 팩에서 tertiary였던 "※ 오락용 타로 해석입니다", "좌우로 넘기고, 끌리는 카드를 탭하세요"는 text/secondary로 올립니다. 원칙 4의 오락용 안내는 잘 보여야 해서입니다.

## 3. 글씨 (Typography)

**Noto Sans KR**(OFL, 무료) 하나만 씁니다. 모든 스타일 자간 **-2%**. 팩의 텍스트 스타일 이름은 `Taro/…`입니다.

| 토큰 | 굵기 | 크기 / 줄 간격 | 쓰는 곳 |
|---|---|---|---|
| `Taro/Display` | Bold | 28 / 38 | S-01 "오늘의 타로" |
| `Taro/Title` | Bold | 22 / 32 | 화면 질문 ("어떤 주제가 궁금한가요?", "커리어를 떠올리며 카드 한 장을 골라 주세요") |
| `Taro/Headline` | Bold | 18 / 26 | 카드 이름 · 별자리, 앱바 제목, 시트 제목 |
| `Taro/Body` | Regular | 16 / 26 | 해석 3줄 (가운데 정렬), 입력값, 설명 |
| `Taro/Body Bold` | Bold | 16 / 24 | L 버튼 |
| `Taro/Label` | Medium | 15 / 22 | M 버튼, 주제 칩, 토스트 |
| `Taro/Caption` | Regular | 13 / 19 | 안내문 · 보조 글 · 오락용 안내 · 오류 문구 |
| `Taro/Caption Bold` | Bold | 13 / 19 | 입력 라벨 |

- 해석 3줄은 `Taro/Body` 가운데 정렬, 90자 이내 (PRD 원칙 3).
- 세리프 글꼴은 쓰지 않습니다.

## 4. 간격 · 모서리 · 그림자

### 화면 틀 (375 × 812)

| 항목 | 값 |
|---|---|
| 좌우 여백 | 20px (본문 폭 335px) |
| 위 상태 표시줄 자리 | 44px |
| 아래 홈 표시줄 자리 | 34px |
| 앱바 | 375 × 56, 좌우 16px, 간격 8px |
| 본문 묶음 사이 | 16px (S-02), 14px (S-03) |
| 주제 칩 사이 | 10px (가로 · 세로) |
| M 버튼 2개 사이 | 11px (162 + 11 + 162 = 335) |
| 하단 버튼 영역 (CTA) | 위 12 · 좌우 20 · 아래 34 |

### 모서리

| 대상 | 값 |
|---|---|
| L 버튼 (335×56) | 16px |
| M 버튼 (162×48) | 14px |
| 주제 칩 (105×44) | 22px (알약) |
| 입력칸 · Privacy Notice · 토스트 · 글 상자 | 12px |
| 카드 뒷면 (120×200) | 12px, 안쪽 선 8px |
| 카드 앞면 (160×268) | 10px |
| 결과 카드 · 바텀시트 위쪽 | 24px |
| 디자인 파일의 화면 틀 | 32px (휴대폰 모양 표시용, 구현에는 안 씀) |

### 그림자

| 이름 | 값 | 쓰는 곳 |
|---|---|---|
| `card` | `0 6px 16px rgba(0,0,0,0.12)` | 카드 앞면 |
| `glow` | `0 10px 28px rgba(0,217,89,0.35)` | 덱에서 고른 카드 (S-03-P2) |
| 시트 뒤 어둡게 | inverse `#232427` 55% | 바텀시트 뒤 |

결과 카드 · 입력칸 · 버튼에는 그림자를 쓰지 않습니다 (팩 기준: 흰 카드는 바탕색 차이로만 구분).

## 5. 아이콘

팩의 아이콘은 **20 × 20, 선 두께 1.67px, 끝 둥글게**입니다 (24px 격자 · 선 2px 아이콘을 20px로 줄인 것. lucide 아이콘과 같은 모양, ISC 라이선스).

| 이름 | 쓰는 곳 |
|---|---|
| `icon/chevron-left` | 앱바 뒤로 |
| `icon/download` | [이미지 저장] |
| `icon/share` | [결과 공유] |
| `icon/refresh` | [다시 뽑기] |
| `icon/home` | [처음으로] |
| `icon/lock` | Privacy Notice |
| `icon/copy` | 복사 실패 시트 |

### 주제 아이콘 [결정: SVG 6개 새로 만듦]

팩 메모에 "emoji 아이콘은 실제 구현 시 SVG 아이콘으로 교체"라고만 있고 주제 아이콘은 없어서, 위와 같은 규격으로 6개를 정했습니다.

| 주제 | 아이콘 (lucide 이름) |
|---|---|
| 커리어 | `briefcase` |
| 재물 | `coins` |
| 연애 | `heart` |
| 건강 | `leaf` |
| 학업 | `book-open` |
| 종합 | `sparkles` |

- 칩 안 아이콘 크기 18px, 글자와 간격 4px. 색은 글자와 같게 (기본 text/secondary, 선택 text/primary).
- 공유 메시지 글(텍스트)의 🔮는 글자라서 그대로 둡니다.

## 6. Tailwind v4 · shadcn 토큰 연결

shadcn의 `tailwindCssFile` **한 곳**에만 씁니다. 다크 모드는 기획에 없어 정의하지 않습니다.

```css
@import "tailwindcss";

:root {
  /* shadcn 기본 변수 ← 팩 변수 */
  --background: #f3f3f5;          /* color/bg */
  --foreground: #000000;          /* color/text/primary */
  --card: #ffffff;                /* color/surface */
  --card-foreground: #000000;
  --popover: #ffffff;
  --popover-foreground: #000000;
  --primary: #00d959;             /* color/accent: L 버튼 */
  --primary-foreground: #000000;  /* color/text/on-accent [결정] */
  --secondary: #ffffff;           /* 흰 버튼 */
  --secondary-foreground: #000000;
  --muted: #f6f6f8;               /* color/surface-sub */
  --muted-foreground: #4d4d4e;    /* color/text/secondary */
  --accent: #e6faef;              /* color/accent-soft: 선택 · hover */
  --accent-foreground: #000000;
  --destructive: #e5484d;         /* color/danger */
  --border: #dcdcdd;
  --input: #dcdcdd;
  --ring: #00d959;                /* 포커스 = 초록 2px (입력칸 Focused) */

  /* shadcn 칸이 없는 토큰 */
  --text-tertiary: #979f9b;
  --disabled: #d7d7d7;
  --inverse: #232427;
  --accent-illust: #00de00;
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-text-tertiary: var(--text-tertiary);
  --color-disabled: var(--disabled);
  --color-inverse: var(--inverse);
  --color-accent-illust: var(--accent-illust);

  /* 모서리 */
  --radius-sm: 10px;     /* 카드 앞면 */
  --radius-md: 12px;     /* 입력칸 · 안내 · 토스트 · 카드 뒷면 */
  --radius-lg: 14px;     /* M 버튼 */
  --radius-xl: 16px;     /* L 버튼 */
  --radius-2xl: 24px;    /* 결과 카드 · 바텀시트 */
  --radius-4xl: 9999px;  /* 주제 칩 */

  --font-sans: "Noto Sans KR", system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;
}

@theme {
  --shadow-card: 0 6px 16px rgba(0,0,0,0.12);
  --shadow-glow: 0 10px 28px rgba(0,217,89,0.35);
}

@layer base {
  * { @apply border-border; }
  body { @apply bg-background text-foreground font-sans antialiased tracking-[-0.02em]; }
}
```

- 색은 **이름 있는 토큰만**: `bg-primary`, `text-muted-foreground`, `bg-inverse`. `bg-[#00d959]` 같은 날값 ✕.

## 7. 컴포넌트

팩의 컴포넌트 이름 그대로 씁니다. shadcn 컴포넌트를 먼저 쓰고, 색 · 크기는 variant(cva)를 고쳐서 맞춥니다.

### 7-1. Button — `Type` × `Size`

| Type | 바탕 | 글자 | 테두리 |
|---|---|---|---|
| Primary | accent | text/on-accent(검정) | 없음 |
| Secondary | surface | text/primary | border 1px |
| Disabled | disabled | text/secondary | 없음 |

| Size | 크기 | 모서리 | 글씨 |
|---|---|---|---|
| L | 335 × 56 (폭 100%) | 16 | Taro/Body Bold |
| M | 162 × 48 | 14 | Taro/Label |

- 속성: `Label`(글자), `Show Icon`, `Icon`(아이콘 바꾸기). 아이콘 20px, 글자와 간격 6px.
- **화면당 Primary 하나.** S-01 [타로 시작] · S-02 [카드 한 장 뽑기]는 L.
- **결과 화면:** [결과 공유]만 Primary M, [이미지 저장] · [다시 뽑기] · [처음으로]는 Secondary M (2×2).
- 이름 · 생년월일 · 주제 중 하나라도 비면 Disabled.
- 포커스: accent 2px 링. 터치 영역 44px 이상.

### 7-2. Input — `State`

| State | 입력칸 테두리 | 값 글자 | 아래 문구 |
|---|---|---|---|
| Default | border 1px | text/tertiary (placeholder) | 없음 |
| Filled | border 1px | text/primary | 없음 |
| Focused | **accent 2px** | text/primary | 없음 |
| Error | **danger 1.5px** | text/primary | Helper, danger, "날짜를 다시 확인해 주세요" |

- 구조: 라벨(Taro/Caption Bold, text/secondary) → 8px → 입력칸(335×52, surface, 모서리 12, 좌우 16) → 8px → Helper.
- 이름: 최대 10자, 닉네임 권장. 생년월일: 실제 날짜만. 전공: 선택 (라벨 "전공 (선택)").
- shadcn: `FieldGroup` › `Field` + `FieldLabel` + `Input` + `FieldDescription`. 오류는 `data-invalid` · `aria-invalid`.

### 7-3. Topic Chip — `State`

- 105 × 44, 모서리 22, 3열 × 2줄, 사이 10px. 주제는 한 개만 (`ToggleGroup type="single"`).
- Default: surface + border 1px + 글자 text/secondary(Taro/Label).
- Selected: accent-soft + **accent 1.5px 테두리** + 글자 text/primary **Bold**. 테두리 두께와 글자 굵기도 같이 바뀌어 색만으로 구분하지 않습니다.
- 아이콘은 §5 주제 아이콘.

### 7-4. Privacy Notice

- surface-sub, 모서리 12, 안쪽 14/16, `icon/lock` 20px + 글자 간격 10px, 글자 Taro/Caption text/secondary.
- S-02 문구: "입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요."
- S-03 문구: "정보는 저장되지 않아요. [처음으로]를 누르면 바로 지워져요."
- shadcn `Alert` + `AlertDescription`.

### 7-5. Toast

- inverse 바탕, 흰 글자 Taro/Label, 모서리 12, 안쪽 14/20. 화면 아래(홈 표시줄 위)에 2초.
- "이미지를 저장했어요" / "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요"

### 7-6. App Bar

- 375 × 56, `icon/chevron-left` + 제목(Taro/Headline) + 오른쪽 20px 빈칸(제목 가운데 맞춤용).
- 속성: `Title`, `Show Back`.

### 7-7. Tarot Card

| 컴포넌트 | 모양 |
|---|---|
| `Tarot Card / Back` | 120 × 200, surface + accent 2px 테두리, 모서리 12. 안쪽 8px 띄운 accent 1px 선(모서리 8), 가운데 accent-soft 원(64) + 8각 별(accent), 위아래 accent 점(8). |
| `Tarot Card / Front` | 160 × 268, 모서리 10, 그림자 `card`. 카드 그림이 꽉 차게. |
| `Tarot Card / 00 The Fool` ~ `21 The World` | 메이저 아르카나 22장. 라이더-웨이트-스미스 1909년판 (팩 출처: "78 Tarot Cards" 파일). |

- 카드 그림 대체 글: `alt="태양 카드"`처럼 한국어 카드 이름.

### 7-8. Result Card (= 저장 이미지)

```
Result Card (335 × 534 · surface · 모서리 24 · 안쪽 28/24 · 간격 16 · 가운데 정렬)
├─ Title       "지민님의 타로 · 커리어"     Taro/Caption · text/secondary
├─ Tarot Card / Front   160 × 268
├─ Meta        "XIX 태양 · 사자자리"       Taro/Headline · text/primary [결정]
├─ Reading     Line 1 · Line 2 · Line 3    Taro/Body · 가운데 · 줄 간격 2
└─ Disclaimer  "※ 오락용 타로 해석입니다"   Taro/Caption · text/secondary [결정]
```

- 속성: `Title`, `Meta`, `Line 1~3`, `Show Major Line`(전공 안 넣으면 끔 → 3번째 줄 생략).
- 해석 줄1 = 카드 × 주제 기본 문장(이름 포함), 줄2 = 별자리 문장, 줄3 = 전공 계열 문장. 전공은 6개 계열로 맞추고, 못 맞추면 줄3 생략.
- 건강 · 재물은 단정하지 않고 돌아볼 관점으로 씁니다.
- **저장 이미지 = 이 카드 그대로, 1080 × 1722 PNG** (335×534 비율, 약 3.22배) **[결정]**. 이미지 맨 아래에 서비스 이름 "오늘의 타로".
- **넣지 않는 것 (원칙 2):** 생년월일, 전공 원문.

### 7-9. Bottom Sheet (저장 · 복사가 안 될 때)

- surface, 위쪽 모서리 24, 안쪽 24/20/34, 간격 16. 뒤는 inverse 55%로 어둡게.
- 저장 안 됨: 제목 "이미지를 길게 눌러 저장해 주세요"(Taro/Headline) + 결과 이미지 미리보기 + Secondary L [닫기].
- 복사 실패: 제목 "아래 글을 길게 눌러 복사해 주세요" + 공유 글 상자(surface-sub, 모서리 12, 안쪽 14, Taro/Caption) + Secondary L [닫기].
- shadcn `Drawer`(휴대폰) / `Dialog`, Title 필수.

### 7-10. 공유 메시지 (글)

```
🔮 {이름}님의 타로 · {주제}
{카드 이름} · {별자리}
{해석 3줄}
※ 오락용 타로 해석입니다
나도 한 장 뽑기 → {시작 링크}
```

- 링크는 시작 화면. 링크에 이름 · 결과는 넣지 않습니다 (원칙 5).
- 공유 메뉴를 취소하면 결과 화면 그대로.

## 8. 카드 뽑기 · 움직임 (F-3) [결정: 팩 흐름 넣기]

팩의 흐름: S-02 [카드 한 장 뽑기] → **S-03-P 카드 고르기** → **S-03-P2 선택됨** → **S-03-D 카드 공개** → S-03 결과.

| 단계 | 화면 | 움직임 |
|---|---|---|
| ① 덱 펼치기 | S-03-P: 질문 "{주제}를 떠올리며 카드 한 장을 골라 주세요"(Taro/Title), 카드 뒷면 22장을 화면 아래 부채꼴로 | 반지름 430, 카드 사이 8°. 진입 시 아래→위로 0.02초씩 차례로 (가운데부터) |
| ② 넘기기 | 안내 "좌우로 넘기고, 끌리는 카드를 탭하세요" + 초록 "Swipe!" 그림 | 덱(wheel) 하나만 회전 (0.45초 따라가기), 손을 떼면 속도 반영 후 8° 단위로 멈춤 |
| ③ 고르기 | S-03-P2: "선택한 카드를 뒤집어 볼게요", 고른 카드가 가운데로 (180×300, `glow` 그림자), 나머지 45% 흐리게 | 0.5초, 1.7배 |
| ④ 뒤집기 | S-03-D: "XIX 태양이 나왔어요" + 카드 앞면 | Y축 180° 회전 0.6초 (반쯤 돌면 옆면만 보임) |
| ⑤ 결과로 | S-03 | 카드가 결과 카드 자리로 0.5초(FLIP), 해석 줄이 0.08초씩 차례로 |

- 앞면은 22장 중 **무작위**(고른 위치와 상관없음), **정방향**만.
- `transform` · `opacity`만 움직입니다. `prefers-reduced-motion`이면 4배 빠르게.
- 기획서 F-3 "뒤집기 1초 이내"는 ④ 뒤집기(0.6초)만 기준으로 봅니다. 고르기 단계가 생긴 건 기획서와 다른 점이라 §11에 적어 둡니다.

## 9. 화면별 적용

| 화면 | 주인공 | 주 버튼 |
|---|---|---|
| S-01 시작 (F-1) | "오늘의 타로"(Display) + 카드 앞면 3장(17 별 · 18 달 · 19 태양) 부채꼴 + 설명 2줄 | L [타로 시작] |
| S-02 내 정보 · 주제 (F-2) | 앱바 "나에 대해 알려 주세요" + 입력 3개 + "어떤 주제가 궁금한가요?" + 주제 칩 6개 + Privacy Notice | L [카드 한 장 뽑기] (Disabled → Primary) |
| S-03-P · P2 · D (F-3) | 카드 덱 · 고른 카드 · 공개 | 없음 |
| S-03 결과 (F-4~F-7) | Result Card | M [결과 공유] (Primary) + Secondary M 3개 |
| S-03 상태 | 토스트 2종, 바텀시트 2종 | — |

- 화면 아래 "※ 오락용 타로 · 정보는 저장 안 해요"(S-01)는 Taro/Caption text/secondary.
- [다시 뽑기] → S-02 주제 선택부터 (입력한 정보는 유지). [처음으로] → 정보 지우고 S-01.

## 10. Do's and Don'ts

### Do
- 바탕은 bg, 담는 것은 흰 surface.
- 글꼴은 Noto Sans KR 하나, 자간 -2%.
- 화면당 초록 Primary 버튼 하나, 그 위 글자는 검정.
- 선택 표시는 accent-soft 바탕 + accent 테두리 + 굵은 글자.
- 🔒 안내와 "오락용" 표시는 text/secondary로 잘 보이게, 항상.
- 카드 그림은 라이더-웨이트-스미스 22장만.

### Don't
- 초록 글자 ✕ (대비 1.90). 초록 버튼 위 흰 글자 ✕.
- text/tertiary를 안내문 · 본문에 ✕ (placeholder · 장식만).
- 세리프 글꼴, 파스텔 주제 색, 종이 질감 장식 ✕ (v0.1 스타일).
- 결과 카드 · 저장 이미지 · 공유 글에 생년월일 · 전공 원문 ✕.
- 날값 색, `space-y-*`, 컴포넌트 색을 `className`으로 덮어쓰기 ✕.
- 레퍼런스(uibowl) 화면의 그림 · 캐릭터 · 브랜드 요소 ✕ (팩도 구조만 참고).

## 11. 접근성 체크

| 항목 | 기준 |
|---|---|
| 글자 대비 | 본문 4.5 이상: text/primary · text/secondary만 글자색. 초록 버튼 위는 검정(11.07). |
| 터치 영역 | 버튼 · 칩 44px 이상 (칩 44, M 버튼 48, L 버튼 56) |
| 포커스 | 버튼 · 입력칸 · 칩 · 덱 카드에 accent 2px 링 |
| 색만으로 구분 ✕ | 선택 칩은 테두리 두께 + 굵은 글자, 오류는 문구 함께 |
| 움직임 | `prefers-reduced-motion`이면 4배 빠르게 |
| 대체 글 | 카드 그림 `alt="태양 카드"`, 장식 그림은 `aria-hidden` |
| 덱 고르기 | 스와이프 못 하는 사람을 위해 좌우 버튼 · 키보드 화살표로도 넘길 수 있게 |

## 12. 아직 정하지 않은 것 · 알려진 문제

- **오류 글자 대비:** danger `#E5484D` 글자는 흰 바탕에서 3.91 (본문 기준 4.5 미달). 팩에 더 진한 빨강이 없어 그대로 두고, 테두리 + 문구로 함께 알립니다. 더 진한 빨강을 정할지 결정이 필요합니다.
- **placeholder 대비:** text/tertiary 2.71. 입력칸 위에 라벨이 따로 있어 placeholder는 보조로만 씁니다.
- **기획서와 다른 점:** ① 카드 고르기 단계 추가(§8), ② 저장 이미지 1080×1722(§7-8). `TARO_02` F-5 · `TARO_04` 저장 이미지 숫자는 1080×1722로 같이 고쳤습니다.
- **카드 그림 저작권:** 라이더-웨이트-스미스 1909년판. 그림 작가 파멜라 콜먼 스미스는 1951년 사망 → 사후 70년이 지나 보호기간이 끝났습니다. 다만 이후 재출판본의 새 색칠 · 디자인에는 권리가 있을 수 있어, 쓰는 파일이 1909년판 스캔인지 확인이 필요합니다.
- **accent-strong:** 팩에서 accent와 같은 값(`#00D959`)입니다. 진하게 쓸 곳이 생기면 다시 정합니다.
- **다크 모드:** 기획에 없어 정의하지 않았습니다.
- **shadcn 프로젝트 설정:** `base`(radix / base), 아이콘 라이브러리(lucide 권장)는 `npx shadcn@latest info`로 확인한 뒤 토스트(`toast` vs `sonner`)를 정합니다.
