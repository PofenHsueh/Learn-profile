# Sass
###### tags: `前端`
## 什麼是Sass
- Sass 全名爲 Syntactically Awesome StyleSheets，是一種 CSS 的擴充語言，即為 CSS 的超集合 。
- 預處理器有三種:
    1. Sass/Scss
    2. Less
    3. Stylus
## 為什麼要使用Sass
- 為了解決在大型專案時傳統 CSS 會遇到的重複、可維護性差等問題。
- 可以撰寫**簡潔**、**富語意（expressive）**、**重複性佳（reusable）**、**可維護性佳**和**可延展性佳**的 CSS 程式碼。
## 與CSS的差異
- CSS 預處理器（Sass）相對於 CSS 算是較高階的語法，需要另外編譯成 CSS，瀏覽器才看得懂。
## Sass與Scss的差別
 Sass 有 Sass 與 Scss 兩種格式
- Sass
    1. 使用縮排區隔程式碼（兩個空白）
    2. **沒有分號、大括號、語法中要加空白**
    3. 無法相容原生 CSS
    4. 檔名為 `.sass`
```bash=
.text-primary
  color: #007bff
```
- Scss
    1. 使用大括號區隔程式碼
    2. **可完全相容原生 CSS**
    3. 檔名為 `.scss`
```bash=
.text-primary{
  color: #007bff;
}
```
## 建立編譯環境
Sass/Scss需要另外編譯成 CSS，瀏覽器才看得懂。
1. 若使用Visual Studio Code可安裝 **Live Sass Compailer** ，按下 Watch Sass就可以進行編譯。
    - ![](https://i.imgur.com/m1aFfX7.png)
    - ![](https://i.imgur.com/PoTtr69.png)
2. 亦可下載prepros進行編譯。

## 如何使用
### @import檔案
- Sass/Scss可將檔案分割成各個部分，並組織成各個獨立的功能，以符號  **_**  作爲這些檔案名稱中的前綴符號，加入前綴符號的這些檔案就不會直接被編譯。
    - ![](https://i.imgur.com/k4WwIH7.png)
 - 所有引入的 Sass/Scss 檔案都將引入到主要的Sass/Scss檔案中（Ex.index.scss），再將Sass/Scss檔案彙整編譯成一隻CSS檔。
- @import檔案除了對於架構的組織上更有邏輯也較好管理，也能減少反覆撰寫相同的程式。
* Sass/Scss是由上至下編譯，要注意@import檔案的**順序**，以免出錯。
Ex.index.scss
    - ![](https://i.imgur.com/N9T8GgF.png)

### 變數（variable）
將變數視為一種存儲要在樣式表中**重複使用**的信息的方法。
**使用該$符號使某物成為變量。**
1. 格式：
   * 數值（Numbers）
     * 若變數爲**數值與單位**的組合仍然爲數值型態。Ex. 10、20px、3em。 
   * 字串（Strings）
     * 不論是否包含引號 (' ')，皆屬於字串型態。Ex. 'test' 。
   * 顏色
     * Ex. red、#72bcd4。
   * 布林（Boolean） 
     * Ex. true、false。
   * 空值（Null） 
     * Ex. null。 

>scss
```bash=
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

>編譯後css
```bash=
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```
2. 支援運算
>scss

![](https://i.imgur.com/GA9piC2.png)

>編譯後css

![](https://i.imgur.com/AYJjf7F.png)

### 巢狀
將CSS selector巢狀化，**降低父元素重複性**。
1. 使用`{}`頭尾包覆下一層class。
2. 使用`＆`選擇上一層selector
```bash=
.btn-primary{
  background-color:$primary-color;
  border-color:$primary-color;
  color:white;
  &:hover{
    background-color:darken($primary-color,15%);
  }
}
```
- 在巢狀中不僅只有 child selectors 可以使用，還可以使用在相同的 Properties 上。
>scss

```bash=
.parent {
  font : {
    family: Roboto, sans-serif;
    size: 12px;
    decoration: none;
  }
}
```
>編譯後的CSS

```bash=
.parent {
  font-family: Roboto, sans-serif;
  font-size: 12px;
  font-decoration: none;
}
```
### @mixin
當CSS設定經常性地被重複使用，甚至可以根據不同「參數」對應出相似的樣式，就可以將這段設定獨立寫成一個 mixin 方便取用。
- 如何撰寫mixin
    1. 先建立一個_mixin.scss，在檔案裡撰寫需要的mixin。
    2. 使用 **@include** 來混入。
```bash=
@mixin 名稱(參數1,參數2,參數3) {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  font-weight: 500;
  font-size: 參數1;
  line-height: 參數3;
  color: 參數2;
}
```
>Scss
>_mixin.scss

```bash=
@mixin limit($color, $size, $line) {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  font-weight: 500;
  font-size: $size;
  line-height: $line;
  color: $color;
}
```
```bash=
h2 {
  @include limit($font-color, 18px, 20px);
}
```
>編譯後CSS

```bash=
h2 {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  font-weight: 500;
  font-size: 18px;
  line-height: 20px;
  color: #0000ff;
}
```
- 可以利用mixin製作RWD網頁
    1. 將@media尺寸的大小寫在_mixin.scss
    2. 使用 **@content**去撰寫@media裡面的css。
> _mixin.scss
```bash=
@mixin pad {
  @media screen and(min-width:450px) and (max-width: 1024px) {
    @content;
  }
}

@mixin web {
  @media screen and(min-width:1100px) and (max-width: 1440px) {
    @content;
  }
}
```
```bash=
//需要用到@media調整尺寸的地方

@include 名稱{
  在此寫css
}
```

>以下為h3在各個尺寸px值不同的範例。
>scss
>
```bash=
h3 {
  padding: 10px;
  font-size: 20px;
  @include pad {
    font-size: 25px;
  }
  @include web {
    font-size: 30px;
  }
}
```

>編譯後CSS

```bash=
h3 {
  padding: 10px;
  font-size: 20px;
}

@media screen and (min-width: 450px) and (max-width: 1024px) {
  h3 {
    font-size: 25px;
  }
}

@media screen and (min-width: 1100px) and (max-width: 1440px) {
  h3 {
    font-size: 30px;
  }
}
```
### @extend
為了避免要一直重寫同一組相同的 CSS 樣式 **@extend** 能夠將重複的樣式整理在一起。
- 如何撰寫extend
    1. 先建立一個_extend.scss檔案，接著在檔案裡撰寫。
    2. 使用%符號。
    3. 使用`@extend`將樣式名稱寫入。

>_extend.scss

```bash=
%font-style {
  background-color: gainsboro;
  color: $text-primary;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  font-size: 30px;
  margin: 20px;
}
```
 > @extend混入
```bash=
.font {
  @extend %font-style;
}
```
### @for
- Sass/Scss提供的for迴圈運算，其概念與一般程式中的for迴圈概念相同，需給定迴圈的**起始值**與**終止值**。
- 以符號`@for`進行迴圈運算。
```bash=
@for $i from $begin through $end {
      /* Declarations */
  }
```
- 變數 `$i` 僅作爲清單 (List) 中元素，都是**編號**。
- 變數 `$begin` 與 `$end` 作爲迴圈的起始點與終止點。
- 關鍵字**through**與**to**可以交換使用。
    - 假設`$begin`值為1，`$end`值為5
        - though
            - 1，2，3，4，5
        - to
            - 1，2，3，4
- 變數 `$i` 在迴圈中必須以`#{ $i }`來顯示
>scss
```bash=
@for $i from 1 through 3 {
  .box-#{ $i } {
    background-color: lighten(blue, $i * 5%);
    border: 1px solid darken(grey, $i * 2%);
  }
} 
```
>css
```bash=
.box-1 {
  background-color: #1a1aff;
  border: 1px solid #7b7b7b;
}

.box-2 {
  background-color: #3333ff;
  border: 1px solid #767676;
}

.box-3 {
  background-color: #4d4dff;
  border: 1px solid #717171;
}
```
### @each
- Sass/Scss提供的each迴圈針對清單 (List) 中的每一項值進行迭代運算。
- 以符號 `@each` 進行迴圈運算。
```bash=
@each $item in $list {
      /* Declarations */
  }
```
- 變數 `$item` 將動態代入 `$list` 的每一項進入迴圈。

>scss
```bash=
$sizes: (
  "sm": 15px,
  "lg": 20px,
  "xl": 25px,
);

@each $key, $value in $sizes {
  .size-#{ $key } {
    font-size: $value;
  }
}
```
>css
```bash=
.size-sm {
  font-size: 15px;
}

.size-lg {
  font-size: 20px;
}

.size-xl {
  font-size: 25px;
}
```
## Vue.js中使用Sass/Scss
### 建立vue.js
- CLI建立時可選擇是否需要預處理。
![](https://i.imgur.com/ZlbyI33.png)
![](https://i.imgur.com/gVMoXET.png)
### 設定
- 建立一個Scss資料夾，裡面放所有的Scss檔案。
    - ![](https://i.imgur.com/0k8kyaC.png)
- 建立vue.config.js檔案
    - ![](https://i.imgur.com/dLK6o6v.png)
- 在vue.config.js中配置，並重啟專案，即可在.vue檔中使用Scss。
```bash=
module.exports = {
  css: {
    loaderOptions: {
      scss: {
        prependData: `@import "@/assets/scss/index.scss";`, //檔案位置
      },
    },
  },
};
```












