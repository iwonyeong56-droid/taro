---
name: 오늘의 타로
version: 0.1
theme: light
base-style: luma          # shadcn style: pill 버튼 · 부드러운 겹그림자 · 넉넉한 여백
viewport: mobile-first    # 360px 기준, 본문 최대 폭 440px
colors:
  canvas: "#fff3e7"
  ink: "#030302"
  white: "#ffffff"
  linen: "#f7f7f7"
  cloud: "#efefef"
  ash: "#e1e1e1"
  stone: "#bebbba"
  mocha: "#6b6966"
  graphite: "#41413f"
  mint: "#9bd8a9"
  marigold: "#fde99b"
  periwinkle: "#b8caf5"
  rose: "#f7c5cc"
  sky: "#9ed4ef"
  papaya: "#ff4500"
  error: "#b42318"
typography:
  display-family: "Gowun Batang, Noto Serif KR, serif"
  body-family: "Pretendard, system-ui, -apple-system, 'Apple SD Gothic Neo', 'Malgun Gothic', sans-serif"
rounded:
  sm: 8px
  md: 12px
  lg: 14px
  xl: 24px
  pill: 9999px
spacing:
  unit: 4px
  gutter: 20px
  section: 40px
components:
  button-primary: { fill: ink, text: white, radius: pill, height: 52px }
  button-secondary: { fill: white, text: ink, border: ash, radius: lg, height: 48px }
  card-result: { fill: white, radius: xl, padding: 24px, shadow: float }
  input: { fill: white, border: ash, radius: lg, height: 48px }
  topic-chip: { fill: white, selected-fill: "topic color", radius: pill, height: 44px }
---

# 오늘의 타로 — Design Guide

> **디지털 스크랩북 속 타로 한 장.** 따뜻한 종이 위에 카드 한 장을 올려 둔 듯한, 손으로 만든 느낌의 모바일 웹.

이 문서는 레퍼런스(디지털 스크랩북 콜라주 스타일 가이드)의 **분위기와 수치 체계**를 가져와, 타로카드 서비스 기획 문서(`TARO_01_PRD` ~ `TARO_04_와이어프레임`)에 맞게 다시 정리한 것입니다. 레퍼런스 브랜드의 이름·로고·일러스트는 쓰지 않습니다.

구현은 **Tailwind CSS v4 + shadcn/ui**를 기준으로 합니다. 토큰 → shadcn 변수 연결, 컴포넌트 규칙은 아래 각 장에 있습니다.

## 1. 디자인 방향

| 기획에서 온 요구 | 디자인으로 푸는 방법 |
|---|---|
| 로그인 없이 1분 안에 끝 (PRD 1) | 한 화면에 한 가지 일. 화면마다 큰 버튼은 하나(검은 알약 버튼). |
| "내 얘기" 같은 해석 (PRD 2) | 결과 카드에 이름·별자리·주제를 **배지**로 붙여, 나를 위해 만든 카드처럼 보이게. |
| 개인정보를 남기지 않음 (원칙 1) | 🔒 안내를 입력칸 바로 아래·결과 아래에 **항상 같은 모양**(Alert)으로. 숨기지 않는다. |
| 이미지 한 장으로 공유 (F-5·F-6) | 결과 카드 = 저장 이미지. 카드 하나가 그대로 1080×1350 이미지가 되도록 비율을 맞춘다. |
| 오락용 해석 (원칙 4) | 신비롭고 무서운 분위기(검정·보라 네온·불길한 빨강) 대신 **밝고 다정한 종이 질감**. |

**한 줄 원칙:** 종이(Canvas) 위에 흰 카드, 글씨는 잉크(Ink), 장식은 파스텔, 행동은 검은 알약 버튼.

## 2. 색 (Colors)

### 2-1. 기본 색

| 이름 | 값 | 역할 | 대비 (WCAG) |
|---|---|---|---|
| Canvas | `#fff3e7` | 모든 화면의 배경. 따뜻한 종이색. | — |
| Ink | `#030302` | 본문·제목 글자, 주 버튼 바탕 | Canvas 위 **18.89** |
| White | `#ffffff` | 카드·입력칸 바탕, 잉크 버튼 위 글자 | Ink 위 **20.63** |
| Graphite | `#41413f` | 소제목, 강조된 보조 글자 | Canvas 위 **9.37** |
| Mocha | `#6b6966` | 설명 글자, 안내문, 입력 도움말 (레퍼런스 Stone 대신) | Canvas 위 **5.01** · White 위 5.47 |
| Stone | `#bebbba` | **글자 금지.** 비활성 테두리, 장식 점선만 | Canvas 위 1.75 ✕ |
| Ash | `#e1e1e1` | 테두리, 구분선 | (선 전용) |
| Cloud | `#efefef` | 눌림·hover 바탕 | — |
| Linen | `#f7f7f7` | 보조 바탕 (S-02 입력 영역 묶음) | — |
| Error | `#b42318` | 생년월일 오류 등 입력 오류 글자·테두리 | Canvas 위 **6.02** |

### 2-2. 파스텔 (주제 색)

주제 6개(PRD 4)에 파스텔을 하나씩 정합니다. 선택된 주제 칩, 결과 카드의 주제 배지, 배경 콜라주 조각에 씁니다. **글자는 항상 Ink**로 올립니다.

| 주제 | 색 이름 | 값 | Ink 글자 대비 |
|---|---|---|---|
| 💼 커리어 | Periwinkle | `#b8caf5` | 12.58 |
| 💰 재물 | Marigold | `#fde99b` | 17.00 |
| 💕 연애 | Rose | `#f7c5cc` | 13.57 |
| 🌿 건강 | Mint | `#9bd8a9` | 12.57 |
| 📚 학업 | Sky | `#9ed4ef` | 12.89 |
| ✨ 종합 | Marigold → Periwinkle 그라데이션 | `linear-gradient(135deg, #fde99b, #b8caf5)` | — |

- Rose는 레퍼런스에 없던 색이라 새로 정했습니다 (연애 주제용). 나머지는 레퍼런스 파스텔을 그대로 씁니다.
- 파스텔은 **작은 면적**(칩·배지·조각)에만. 화면 전체 바탕을 파스텔로 칠하지 않습니다.

### 2-3. 포인트 색

| 이름 | 값 | 쓰는 곳 | 쓰면 안 되는 곳 |
|---|---|---|---|
| Papaya | `#ff4500` | 결과 카드의 얇은 액자 테두리(2px), 카드 뒤집기 순간의 반짝 효과, 손그림 동그라미 | 버튼 바탕, 글자 (흰 글자 대비 3.44 ✕) |

## 3. 글씨 (Typography)

레퍼런스의 "세리프 제목 + 산세리프 UI" 대비를 그대로 쓰되, **한글이 되는 무료 글꼴**로 바꿉니다.

| 역할 | 글꼴 | 대체 | 쓰는 곳 |
|---|---|---|---|
| Display (세리프) | **Gowun Batang** (OFL) | Noto Serif KR → serif | 화면 제목, 카드 이름(예: "XIX 태양"), 결과 카드 제목 |
| Body (산세리프) | **Pretendard** (OFL) | system-ui, Apple SD Gothic Neo, Malgun Gothic | 버튼·입력칸·해석 문장·안내문 등 나머지 전부 |

### 타입 스케일 (모바일 기준)

레퍼런스는 데스크톱 기준(최대 66px)이라 모바일 360px에 맞게 줄였습니다. 한글은 자간을 크게 좁히면 글자가 붙어 보여서, 음수 자간을 레퍼런스의 절반 정도만 씁니다.

| 토큰 | 글꼴 | 크기 | 굵기 | 줄 간격 | 자간 | 쓰는 곳 |
|---|---|---|---|---|---|---|
| `display` | Serif | 36px | 400 | 1.15 | -0.9px | S-01 "오늘의 타로" |
| `heading` | Serif | 28px | 400 | 1.2 | -0.56px | 화면 제목 ("나에 대해 알려 주세요") |
| `card-name` | Serif | 24px | 400 | 1.25 | -0.36px | 결과 카드 이름 ("XIX 태양") |
| `subheading` | Sans | 20px | 700 | 1.4 | -0.4px | 결과 카드 머리 ("지민님의 타로 · 커리어") |
| `reading` | Sans | 17px | 500 | 1.6 | -0.17px | 해석 3줄 (가장 잘 읽혀야 하는 글) |
| `body` | Sans | 16px | 400 | 1.5 | -0.16px | 입력 라벨, 일반 글 |
| `body-sm` | Sans | 14px | 400 | 1.5 | 0 | 안내문(🔒), 도움말 |
| `caption` | Sans | 12px | 500 | 1.5 | 0.12px | "※ 오락용 타로 해석입니다", 배지 |

- 세리프는 **24px 이상**에서만. 버튼·입력칸·본문에는 쓰지 않습니다.
- 해석 3줄(`reading`)은 90자 안팎이라(PRD 원칙 3) 360px 화면에서 줄당 약 18자 → 6~7줄로 보입니다. 줄 간격 1.6으로 답답하지 않게 합니다.

## 4. 간격 · 모양 · 그림자

### 간격 (4px 단위)

| 토큰 | 값 | 쓰는 곳 |
|---|---|---|
| `gap-1` | 4px | 배지 안 아이콘과 글자 |
| `gap-2` | 8px | 주제 칩 사이, 배지 사이 |
| `gap-3` | 12px | 버튼 2개 나란히 |
| `gap-4` | 16px | 입력칸(Field) 사이 |
| `gap-5` | 20px | 화면 좌우 여백(gutter) |
| `gap-6` | 24px | 카드 안쪽 여백 |
| `gap-10` | 40px | 화면 안 큰 묶음 사이 (레퍼런스 96~120px를 모바일에 맞게 줄임) |

- 화면 좌우 여백 20px, 본문 최대 폭 440px(가운데 정렬). 넓은 화면에서도 휴대폰 화면처럼 보입니다.
- 세로로 쌓을 때는 `flex flex-col gap-*`. `space-y-*`는 쓰지 않습니다 (shadcn 규칙).

### 모서리

| 대상 | 값 | Tailwind 클래스 (§6 매핑) |
|---|---|---|
| 배지 · 주제 칩 · 주 버튼 | 9999px (알약) | `rounded-4xl` / `rounded-full` |
| 결과 카드 · 시작 화면 카드 | 24px | `rounded-xl` |
| 입력칸 · 보조 버튼 · 안내 상자 | 14px | `rounded-lg` |
| 토스트 · 이미지 미리보기 | 24px | `rounded-2xl` |
| 작은 장식 | 8px | `rounded-sm` |

0px 모서리(각진 카드·버튼)는 쓰지 않습니다.

### 그림자 (레퍼런스 값 그대로)

| 이름 | 값 | 쓰는 곳 |
|---|---|---|
| `float` | `rgba(0,0,0,0.01) 0 50px 40px 0, rgba(0,0,0,0.02) 0 50px 40px 0, rgba(0,0,0,0.05) 0 20px 40px 0, rgba(0,0,0,0.08) 0 3px 10px 0` | 결과 카드, 시작 화면의 카드 뒷면 |
| `lift` | `rgba(0,0,0,0.1) 0 12px 12px 2px, rgba(0,0,0,0.06) 0 2px 4px -1px` | 주 버튼 누를 때, 이미지 미리보기 Dialog |
| `soft` | `rgba(0,0,0,0.08) 0 4px 16px 0` | 입력 영역 묶음, 토스트 |
| `subtle` | `rgba(0,0,0,0.1) 0 1px 3px 0, rgba(0,0,0,0.1) 0 1px 2px -1px` | 상단 뒤로가기 줄, 선택된 주제 칩 |

한 겹짜리 진한 그림자는 쓰지 않습니다.

## 5. 질감 · 장식 (Collage)

- **종이 조각:** 찢어진 가장자리의 파스텔 조각을 화면 모서리·카드 뒤에 1~2개. 그 화면의 주제 색을 씁니다 (S-03 결과: 고른 주제의 색).
- **점 격자:** Canvas 위에 아주 옅은 점 격자(점 Stone, 투명도 30%, 간격 16px)를 S-01 배경에만.
- **카드 뒷면:** Ink 바탕 + Marigold 별·달 선 그림 + 2px Papaya 안쪽 테두리. 시작 화면과 뽑기 전 카드에 같은 그림을 씁니다.
- 장식은 `aria-hidden="true"`, 글자 뒤에 겹치지 않게 둡니다.
- 카드 앞면 그림(메이저 아르카나 22장)은 PRD 8 '카드 그림 출처'가 정해진 뒤 이 질감에 맞춰 그립니다 (§11).

## 6. Tailwind v4 · shadcn 토큰 연결

shadcn의 `tailwindCssFile`(보통 `src/index.css` 또는 `app/globals.css`) **한 곳**에만 씁니다. 다크 모드는 기획에 없어 `.dark`는 정의하지 않습니다 (§11).

```css
@import "tailwindcss";

:root {
  /* shadcn 기본 변수 ← 이 문서의 색 */
  --background: #fff3e7;          /* Canvas */
  --foreground: #030302;          /* Ink */
  --card: #ffffff;
  --card-foreground: #030302;
  --popover: #fff3e7;
  --popover-foreground: #030302;
  --primary: #030302;             /* 주 버튼 = 검은 알약 */
  --primary-foreground: #ffffff;
  --secondary: #ffffff;           /* 보조 버튼 = 흰 바탕 + Ash 테두리 */
  --secondary-foreground: #030302;
  --muted: #f7f7f7;               /* Linen */
  --muted-foreground: #6b6966;    /* Mocha (Stone 아님) */
  --accent: #efefef;              /* Cloud: hover·눌림 */
  --accent-foreground: #030302;
  --destructive: #b42318;         /* Error */
  --border: #e1e1e1;              /* Ash */
  --input: #e1e1e1;
  --ring: #030302;                /* 포커스 테두리는 잉크 */

  /* shadcn 칸이 없는 토큰 */
  --graphite: #41413f;
  --stone: #bebbba;
  --primary-active: #41413f;      /* 주 버튼 눌림 */
  --papaya: #ff4500;
  --topic-career: #b8caf5;
  --topic-money: #fde99b;
  --topic-love: #f7c5cc;
  --topic-health: #9bd8a9;
  --topic-study: #9ed4ef;
  --topic-all: linear-gradient(135deg, #fde99b, #b8caf5);
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
  --color-primary-active: var(--primary-active);
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
  --color-graphite: var(--graphite);
  --color-stone: var(--stone);
  --color-papaya: var(--papaya);
  --color-topic-career: var(--topic-career);
  --color-topic-money: var(--topic-money);
  --color-topic-love: var(--topic-love);
  --color-topic-health: var(--topic-health);
  --color-topic-study: var(--topic-study);

  /* 모서리: 이 문서 단계 → shadcn 컴포넌트가 쓰는 클래스 */
  --radius-sm: 8px;      /* 작은 장식 */
  --radius-md: 12px;     /* 메뉴 항목 */
  --radius-lg: 14px;     /* 입력칸 · 보조 버튼 · 안내 상자 */
  --radius-xl: 24px;     /* 카드 · Dialog */
  --radius-2xl: 24px;    /* 토스트 · 이미지 미리보기 */
  --radius-3xl: 24px;
  --radius-4xl: 9999px;  /* 배지 · 칩 (알약) */

  /* 글꼴 */
  --font-sans: "Pretendard", system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;
  --font-serif: "Gowun Batang", "Noto Serif KR", serif;
}

@theme {
  /* 그림자: 겹그림자 그대로 (Tailwind 그림자 이름을 덮어씀) */
  --shadow-xs: 0 0 #0000;
  --shadow-sm: rgba(0,0,0,0.1) 0 1px 3px 0, rgba(0,0,0,0.1) 0 1px 2px -1px;
  --shadow-md: rgba(0,0,0,0.08) 0 4px 16px 0;
  --shadow-lg: rgba(0,0,0,0.1) 0 12px 12px 2px, rgba(0,0,0,0.06) 0 2px 4px -1px;
  --shadow-xl: rgba(0,0,0,0.01) 0 50px 40px 0, rgba(0,0,0,0.02) 0 50px 40px 0, rgba(0,0,0,0.05) 0 20px 40px 0, rgba(0,0,0,0.08) 0 3px 10px 0;

  /* 카드 뒤집기 (F-3: 1초 이내) */
  --animate-card-flip: card-flip 0.8s cubic-bezier(0.2, 0.7, 0.2, 1) both;
  @keyframes card-flip {
    from { transform: perspective(900px) rotateY(180deg); }
    to   { transform: perspective(900px) rotateY(0deg); }
  }
}

@layer base {
  * { @apply border-border; }
  body { @apply bg-background text-foreground font-sans antialiased; }
}

@media (prefers-reduced-motion: reduce) {
  .animate-card-flip { animation: none; }
}
```

- 색은 **이름 있는 토큰만** 씁니다: `bg-primary`, `text-muted-foreground`, `bg-topic-love`. `bg-[#fde99b]`, `text-gray-500` 같은 날값은 쓰지 않습니다.
- shadcn style은 **luma**로 시작합니다 (알약 버튼·부드러운 겹그림자·넉넉한 여백이 이 문서와 가장 가까움). 세리프 제목은 `font-serif`로 따로 지정합니다.

## 7. 컴포넌트 규칙

shadcn 컴포넌트를 먼저 쓰고, 색·크기는 **variant(cva)를 고쳐서** 맞춥니다. `className`으로는 배치(여백·폭)만 정하고 색·글씨를 덮어쓰지 않습니다.

### 7-1. 버튼 — `Button`

| 종류 | variant | 모양 | 쓰는 곳 |
|---|---|---|---|
| **주 버튼** | `default` | Ink 바탕 · 흰 글자 · 알약 · 높이 52px · 폭 100% · 16px/700 | [타로 시작] · [카드 한 장 뽑기] |
| 보조 버튼 | `secondary` | 흰 바탕 · Ink 글자 · Ash 1px 테두리 · 14px 모서리 · 높이 48px | [이미지 저장] · [결과 공유] |
| 조용한 버튼 | `ghost` | 바탕 없음 · Graphite 글자 · 눌리면 Cloud | [다시 뽑기] · [처음으로] · ← 뒤로 |

- 한 화면에 주 버튼은 **하나만**.
- 상태:
  - 누름: 주 버튼 `bg-primary-active` + `shadow-lg`
  - 비활성: 주 버튼 Ash 바탕 + Mocha 글자, `disabled`
  - 포커스: Ink 2px 링, 2px 띄움
- **[카드 한 장 뽑기] 비활성 규칙 (F-2):** 이름·생년월일·주제가 다 채워지기 전엔 `disabled`. 버튼 아래 Mocha 글씨로 "이름 · 생년월일 · 주제를 채우면 뽑을 수 있어요".
- 진행 중 표시: `Button`에 `isLoading`은 없습니다. `Spinner` + `data-icon="inline-start"` + `disabled`로 만듭니다 (이미지 만드는 중).
- 아이콘은 `data-icon="inline-start | inline-end"`, 아이콘 크기 클래스는 붙이지 않습니다.
- 터치 영역은 최소 44×44px.

### 7-2. 입력 — `FieldGroup` · `Field` · `Input`

S-02 정보 입력은 `FieldGroup` 안에 `Field`를 쌓습니다 (`div` + `space-y` 금지).

| 칸 | 컴포넌트 | 규칙 |
|---|---|---|
| 이름 (닉네임 OK) | `Field` + `FieldLabel` + `Input` | 최대 10자 (`maxLength={10}`), 오른쪽에 글자 수 `FieldDescription` |
| 생년월일 | `Field` + `Input type="date"` | 실제 날짜만. 틀리면 `Field data-invalid` + `Input aria-invalid` + Error 색 `FieldDescription` "날짜를 다시 확인해 주세요" |
| 전공 (선택) | `Field` + `Input` | 라벨 옆 `Badge variant="outline"` "선택" |

- 입력칸: 흰 바탕 · Ash 테두리 · 14px 모서리 · 높이 48px · 글자 16px(휴대폰 자동 확대 방지).
- 포커스: 테두리 Ink + Ink 링.
- 입력 영역 전체는 Linen 바탕 카드(`shadow-md`)로 묶습니다.

### 7-3. 주제 선택 — `ToggleGroup`

주제 6개는 **선택지 2~7개 → `ToggleGroup`** 규칙을 따릅니다 (`Button`을 반복해서 직접 선택 상태를 만들지 않음).

- `ToggleGroup type="single"` + `ToggleGroupItem` 6개, 3열 × 2줄 격자, 칩 사이 8px.
- 칩: 알약 · 높이 44px · 흰 바탕 · Ash 테두리 · 이모지 + 글자(14px/500).
- 선택됨: 그 주제 색 바탕(§2-2) + Ink 글자 + `shadow-sm` + Ink 1px 테두리. 색만으로 구분하지 않도록 ✓ 아이콘도 함께.
- 그룹 이름은 `FieldSet` + `FieldLegend` "어떤 주제가 궁금한가요?".

### 7-4. 결과 카드 — `Card` (= 저장 이미지)

와이어프레임 S-03의 카드 영역이 그대로 저장 이미지가 됩니다 (F-5).

```
Card (흰 바탕 · 24px 모서리 · shadow-xl · 안쪽 2px Papaya 액자는 장식)
├─ CardHeader
│   ├─ CardTitle      "지민님의 타로"            subheading
│   └─ CardDescription Badge(주제 색) "💼 커리어"  Badge(outline) "♌ 사자자리"
├─ CardContent
│   ├─ 카드 그림 (2:3 비율, 12px 모서리, 뽑을 때 animate-card-flip)
│   ├─ 카드 이름 "XIX 태양"                      card-name (세리프)
│   └─ 해석 3줄                                  reading, 줄마다 <p>
└─ CardFooter
    └─ "※ 오락용 타로 해석입니다"                  caption, Mocha
```

- `CardHeader` · `CardTitle` · `CardDescription` · `CardContent` · `CardFooter`를 모두 씁니다. 전부 `CardContent`에 몰아넣지 않습니다.
- 화면 카드 비율 = 저장 이미지 비율 **4:5 (1080×1350)**. 360px 화면에서 카드 폭 320px → 높이 400px.
- **카드와 이미지에 넣지 않는 것 (원칙 2):** 생년월일, 전공 원문. 별자리·주제만 배지로.
- 저장 이미지 맨 아래에는 서비스 이름 "오늘의 타로"를 세리프 caption으로 넣습니다.

### 7-5. 배지 — `Badge`

| 쓰는 곳 | variant | 모양 |
|---|---|---|
| 주제 | `secondary` + 주제 색 바탕 | 알약 · 12px/500 · Ink 글자 |
| 별자리 | `outline` | 알약 · Ash 테두리 |
| "선택" 표시 (전공) | `outline` | 알약 · Mocha 글자 |

직접 꾸민 `span`으로 배지를 만들지 않습니다.

### 7-6. 개인정보 안내 — `Alert`

원칙 1의 안내문은 S-02 입력칸 아래, S-03 버튼 아래에 **같은 모양**으로 둡니다.

- `Alert` (기본 variant) + 🔒 자물쇠 아이콘 + `AlertDescription`.
- Linen 바탕 · Ash 테두리 · 14px 모서리 · 14px 글자 · Mocha 글자(자물쇠와 "저장하지 않아요"만 Ink 굵게).
- 문구는 기능명세서의 안내문을 그대로 씁니다. 줄이거나 작게 숨기지 않습니다.

### 7-7. 알림 · 안 될 때 — 토스트 · `Dialog`

| 상황 (기능명세서) | 컴포넌트 | 모양 |
|---|---|---|
| 이미지를 저장했어요 / 결과를 복사했어요 | 토스트 (Base UI 프로젝트는 `toast`, Radix는 `sonner`) | 화면 아래 · Ink 바탕 · 흰 글자 · 24px 모서리 · 2초 |
| 이미지 저장이 안 될 때 | `Dialog` (또는 휴대폰에선 `Drawer`) + `DialogTitle` "이미지를 길게 눌러 저장해 주세요" | 결과 이미지 미리보기 · `shadow-lg` |
| 복사도 실패할 때 | `Dialog` + 메시지 글 상자 | 글 상자 길게 눌러 선택 가능 |

- `Dialog` · `Drawer`에는 반드시 Title을 둡니다 (안 보이게 할 땐 `sr-only`). 겹침 순서(`z-index`)는 직접 정하지 않습니다.

### 7-8. 카드 뽑기 연출 — F-3

- [카드 한 장 뽑기] → 카드 뒷면이 앞면으로 뒤집힘 (`animate-card-flip`, 0.8초, 1초 이내 규칙).
- 뒤집히는 순간 Papaya 반짝 효과 1번. 소리·진동 없음.
- `prefers-reduced-motion`이면 뒤집지 않고 바로 앞면을 보여 줍니다.
- 로딩 화면은 따로 두지 않습니다 (해석은 앱 안 문구라 바로 나옴, 기능명세서).

### 7-9. 화면 머리 · 구분선

- S-02 상단 "← 나에 대해 알려 주세요": 왼쪽 `ghost` 아이콘 버튼 + `heading` 세리프 제목. 줄 아래 그림자 `shadow-sm`.
- 구분선은 `Separator` (Ash 1px). `<hr>`이나 테두리 `div`를 쓰지 않습니다.

## 8. 화면별 적용

| 화면 | 바탕 | 주인공 | 주 버튼 | 장식 |
|---|---|---|---|---|
| S-01 시작 (F-1) | Canvas + 점 격자 | 카드 뒷면 (`shadow-xl`, 살짝 기울임 -4°) + `display` "오늘의 타로" | [타로 시작] | 모서리 파스텔 종이 조각 2개 |
| S-02 내 정보·주제 (F-2) | Canvas | 입력 카드(Linen) + 주제 칩 6개 | [카드 한 장 뽑기] (비활성 → 활성) | 없음 (입력에 집중) |
| S-03 결과 (F-4~F-7) | Canvas | 결과 카드 (= 저장 이미지) | 없음. 보조 2개 + 조용한 2개 | 고른 주제 색 종이 조각 1개 (카드 뒤) |

- 공유 메시지 글(와이어프레임 '공유 메시지')은 디자인이 아니라 문구 규칙이라 기능명세서를 따릅니다.

## 9. Do's and Don'ts

### Do
- 모든 화면 바탕은 **Canvas(#fff3e7)**. 카드만 흰색.
- 화면 제목·카드 이름은 **세리프**(Gowun Batang), 나머지는 전부 **Pretendard**.
- 한 화면에 검은 알약 주 버튼은 **하나**.
- 주제마다 정해진 파스텔을 칩·배지·조각에 **같은 색으로** 계속 씁니다.
- 🔒 개인정보 안내와 "오락용 해석" 표시는 **눈에 보이는 크기로 항상** 둡니다.
- 결과 카드는 4:5 비율 그대로 이미지가 되게 만듭니다.
- 카드·떠 있는 요소에는 겹그림자(`shadow-xl`, `shadow-lg`)를 씁니다.

### Don't
- 순수 검정(#000) 글자, 순수 흰(#fff) 화면 바탕 ✕ (글자는 Ink, 바탕은 Canvas).
- Stone(#bebbba)을 글자색으로 ✕ (대비 1.75). 설명 글은 Mocha.
- Papaya 바탕에 흰 글자 ✕ (대비 3.44). Papaya는 액자·반짝임에만.
- 세리프를 버튼·입력칸·24px보다 작은 글에 ✕.
- 파스텔로 화면 전체를 칠하기 ✕, 주제 색을 화면마다 다르게 쓰기 ✕.
- 검정·보라 네온·빨강 경고색으로 무섭고 신비로운 분위기 내기 ✕ (오락용·다정한 톤).
- 결과 카드·저장 이미지·공유 글에 **생년월일**이나 전공 원문 ✕ (원칙 2).
- 날값 색(`bg-[#...]`, `text-gray-500`), `space-y-*`, 컴포넌트 색을 `className`으로 덮어쓰기 ✕.
- 0px 각진 모서리, 한 겹짜리 진한 그림자 ✕.
- 레퍼런스 브랜드의 이름·로고·그림 사용 ✕.

## 10. 접근성 체크

| 항목 | 기준 |
|---|---|
| 글자 대비 | 본문 4.5 이상: Ink·Graphite·Mocha·Error만 글자색 (§2 표의 수치) |
| 터치 영역 | 버튼·칩 44×44px 이상 |
| 포커스 | 모든 버튼·입력칸·칩에 Ink 2px 링 |
| 색만으로 구분 ✕ | 선택된 주제 칩은 ✓ 아이콘 함께, 입력 오류는 문구 함께 |
| 움직임 | `prefers-reduced-motion`이면 카드 뒤집기 없음 |
| 대체 글 | 카드 그림 `alt="태양 카드"`, 장식은 `aria-hidden` |

## 11. 아직 정하지 않은 것 (Known Gaps)

- **카드 앞면 그림 22장:** PRD 8 '카드 그림 출처' 미정. 정해지면 §5 질감에 맞춰 그립니다.
- **글꼴 파일:** Gowun Batang · Pretendard는 무료(OFL)지만, 앱에 파일로 넣을지 웹폰트로 불러올지 정해야 합니다 (이미지 저장 시 글꼴이 그대로 들어가야 함).
- **다크 모드:** 기획에 없어 정의하지 않았습니다. 필요하면 Canvas·Ink를 뒤집은 `.dark` 토큰을 따로 정합니다.
- **종합 주제 색:** 그라데이션은 배지에선 괜찮지만 저장 이미지에서 어떻게 보일지 시안 확인이 필요합니다.
- **shadcn 프로젝트 설정:** `base`(radix / base)와 아이콘 라이브러리는 `npx shadcn@latest info`로 확인한 뒤 토스트(`toast` vs `sonner`)·`asChild` vs `render`를 정합니다.
- **레퍼런스와 다르게 바꾼 것:** 모바일 타입 스케일(최대 36px), 한글 자간 완화, Mocha·Rose·Error 색 추가, 섹션 간격 40px.
