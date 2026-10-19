# Controller contract（骨架的擴充點）

`assets/lesson-template.html` 已包含：樣式、頁面外框、講解面板、練習列（對答案／看答案／換一題）、目錄、工具列（雷射筆、畫筆、橡皮擦、垃圾桶）、鍵盤控制、自動縮放。**你只需要改標示 `[TEMPLATE]` 的區塊。**

## 1. 宣告主題

```js
const DEFS = [
  // [主題編號, 概念頁標題, 概念頁教材出處, 練習頁標題, 練習頁教材出處]
  [1, '時間軸怎麼看', 'L1 課本 p.6', '看圖寫句子：過去、現在、未來', 'L1 課本 p.6'],
];
const TOPIC_NAMES = ['時間軸怎麼看'];   // 目錄用的短名稱，順序同 DEFS
```
主題編號 1～9 對應數字鍵 1～9，第 10 個主題對應 0。

骨架會為每個主題自動產生兩個 `<section class="slide">`：
- `#d{主題}_1` / `#s{主題}_1`：概念頁的圖解區、句子區
- `#d{主題}_2` / `#s{主題}_2`：練習頁的圖解區、句子區

## 2. 寫控制器

```js
CTRL['3_1'] = (() => {        // 主題 3 概念頁
  const svg = svgIn(D(3,1));  // 在圖解區放一個 SVG（viewBox 1600×560）
  ...
  function render() { /* 畫圖 + 改句子 SEN(3,1).innerHTML = ... */ }
  return {
    render,                    // 必填：依目前狀態重畫
    explain: () => `<ol>…</ol>`,   // 必填：講解面板的 HTML（打開時才呼叫）
    reset() { /* 回到初始狀態 */ render(); },   // 必填
    play() {}, stop() {},      // 選填：有 play 才會出現「播放」按鈕
  };
})();

CTRL['3_2'] = (() => {        // 主題 3 練習頁
  ...
  return {
    render,
    answers: () => [ ['paid'] ],           // 每個空格一個陣列，陣列內是所有可接受答案
    explain() { ... },                     // 這一題的逐步講解
    randomize() { /* 隨機換題，圖和句子一起變，最後 render() */ },
    reset() { ... },
    askLabel: '下一題',                    // 選填：按鈕文字，預設「換一題」
  };
})();
```

### 練習頁的句子
空格用 `blank(placeholder, answersArray)` 產生，放在句子字串裡：
```js
SEN(3,2).innerHTML = `Ethan ${blank('pay', ['paid'])} his bill.`;
```
`answers()` 回傳陣列的長度要等於句子裡空格的數量。

### 共用小工具（骨架已有）
- `V(s)` / `T(s)`：把字包成「動詞（藍）」／「時間點（橘）」標籤。可改成該科目的角色顏色。
- `el(tag, attrs, parent, text)`：建立 SVG 元素；`clear(g)`：清空群組。
- `dragOn(target, svg, (p, start) => …)`：讓 SVG 元素可拖曳（自動處理座標轉換與暫停播放）。
- `makeChips` / `chipsIn(diagramEl, 標籤, 選項[], 回呼, 'right')`：圖解區左上（或右上）的選項按鈕。
- `rnd(n)`、`pick(arr)`：隨機。
- `svgIn(host, viewBox)`：在容器裡建 SVG。

### 概念頁 vs 練習頁的圖
同一種圖解建議寫成一個函式 `XxxDiagram(svg, practice)`，用 `practice` 旗標切換：
- 概念頁：可拖曳、顯示狀態標籤（例如「現在進行式」）。
- 練習頁：不可拖曳、**隱藏會洩答案的標籤**，由 `randomize()` 設定狀態。

## 3. 檢查清單
- [ ] 每個練習頁的 `answers()` 在任何隨機狀態下都等於「圖解推出的唯一／可接受答案」
- [ ] `explain()` 不含 `undefined`／`NaN`
- [ ] 句子很長時加 `SEN(...).classList.add('long')`（字級 46px）
- [ ] 有自動播放（`play`）的頁面在 `stop` 裡 `cancelAnimationFrame`／`clearInterval`
