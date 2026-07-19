# Colorable

Take a set color palette and get contrast values for every possible combination – 
useful for finding safe color combinations with predefined colors
and includes pass/fail scores for the
[WCAG accessibility guidelines](http://www.w3.org/TR/WCAG20/#visual-audio-contrast).

## Getting Started

```bash
npm i --save colorable
```

## Usage

Pass an array of color strings or an object with color strings as values. 

```js
var colorable = require('colorable')

var colors = {
  red: 'red',
  green: 'green',
  blue: 'blue'
}

var result = colorable(colors, { compact: true, threshold: 0 })
```

Returns an array of colors with combinations for all other colors and their
[WCAG contrast](http://www.w3.org/TR/WCAG20/#visual-audio-contrast)
values.

```json
[
  {
    "hex": "#FF0000",
    "name": "red",
    "combinations": [
      {
        "hex": "#008000",
        "name": "green",
        "contrast": 1.28483997166146,
        "accessibility": {
          "aa": false,
          "aaLarge": false,
          "aaa": false,
          "aaaLarge": false
        }
      },
      {
        "hex": "#0000FF",
        "name": "blue",
        "contrast": 2.148936170212766,
        "accessibility": {
          "aa": false,
          "aaLarge": false,
          "aaa": false,
          "aaaLarge": false
        }
      }
    ]
  },
  ...
]
```

### Accessibility object

Each key is a boolean value indicating if the color contrast meets the following criteria:
- `aa` - greater than 4.5 (for normal sized text)
- `aaLarge` - greater than 3 ([for bold text or text larger than 24px](http://www.w3.org/TR/WCAG20/#larger-scaledef))
- `aaa` - greater than 7 
- `aaaLarge` - greater than 4.5 

---

## Options

### `compact`

_Type: Boolean (default: `false`)_

If set to `true`, the result will be a smaller object that only includes hex value color strings, a name for each color (if an object is passed to the function), contrast, and accessibility values.
When set to `false`, the result also includes the entire [harthur/color](https://www.npmjs.com/package/color) object for each color, which includes other properties and methods for color manipulation.

### `threshold`

_Type: Number (default: `0`)_

When set, the colorable function only returns combinations that have a contrast above this value. This is useful for only seeing combinations that pass a minimum contrast level.

### `uniq`

_Type: Boolean (default: true)_

When set to `true`, the array of colors is passed through lodash.uniq to remove duplicates.


---

## Griff 버전 (color.griff.co.kr)

배포 사이트는 원본 React/webpack 데모(`docs/`, `webpack.config.js`, `index.js` — 모두 `.vercelignore`)를
쓰지 않고, 손으로 유지하는 단일 정적 파일 **`index.html`**(인라인 CSS + 바닐라 JS)을 그대로 서빙한다.
기능 추가는 이 파일을 직접 편집한다.

이번에 추가된 기능:

- **그리프 프리셋 · Griff Presets** — 폰트 스위처 아래 스와치 칩 그룹(Que 상태색 5·브랜드·바로가기 6·DayBlocks 8).
  칩 클릭 = 글자색 적용, Shift+클릭 또는 우클릭 = 배경색 적용. 색 값은 실제 소스에서 추출
  (Que `globals.css`/`pm-columns.ts`, `menu.ts` accentColor, DayBlocks `tokens.css`).
- **색각 이상 시뮬레이션** — 미리보기(샘플 텍스트)에 SVG `feColorMatrix` 필터(적록 protan/deutan·청황 tritan) 토글.
  근사치이며, 상단 대비 수치·뱃지는 원본 색 기준 그대로 유지한다.
- **커스텀 샘플 문장** — 입력창에 문장을 넣으면 큰/본문/작은 샘플의 첫 문장이 교체된다(비우면 복원).
- **APCA Lc 병기** — WCAG 2 대비 옆에 APCA-W3(Lc) 값을 참고용으로 표시. 등급 판정은 WCAG 2 그대로.
- **파비콘** — 팔레트 계열 SVG(`/favicon.svg`).

MIT License

