# Tailwind css

## 安裝
- 以Vue.js為例
1. `npm install tailwindcss postcss autoprefixer`
2. 建立postcss.config.js檔
    ```bash=
    // postcss.config.js
    module.exports = {
      plugins: {
        tailwindcss: {},
        autoprefixer: {},
      }
    }
    ```
3. 初始化tailwind.config.js檔
    - `npx tailwindcss init`
```bash=
// tailwind.config.js
module.exports = {
  purge: [],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {},
  plugins: [],
}
```
4. 建立tailwind.css
```bash=
@tailwind base;
@tailwind components;
@tailwind utilities;
```
5. import tailwind.css 在main.js
```bash=
import Vue from "vue";
import App from "./App.vue";
import "./assets/tailwind.css";

Vue.config.productionTip = false;

new Vue({
  render: h => h(App)
}).$mount("#app");
```

> tailwind 2 中的postcss版本為8，Vue.js目前不支援（我在寫這篇的時候），所以安裝完會發生錯誤，要將postcss降版才能順利使用。

> 降版本
```bash=
npm uninstall tailwindcss postcss autoprefixer
npm install tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```
## 自定義
- 在tailwind.css中使用
    - 使用`@layer`指令告訴Tailwind一組自定義樣式屬於哪個“桶”。有效層是`base`，`components`，和`utilities`。
    - `@apply`將任何現有實用程序類內聯到您自己的自定義CSS中。
### base
- 基本（或全局）樣式是樣式表開頭的樣式，可為基本HTML元素（例如`<a>`標籤，標題等）設置有用的默認值。

> tailwind.css
```bash=
@layer base {
  h1 {
    @apply text-2xl font-bold text-blue-600;
  }
}
```
>效果
![](https://i.imgur.com/U07G4xe.png)

### components
- 有重複使用到相同css效果時，可將其包成component形式，以`class="名稱"`帶入使用。
>tailwind.css
```bash=
@layer components {
  .text-content {
    @apply text-sm font-bold bg-yellow-300 text-white text-center;
  }
}
```
>只要class="text-content"，就會有以下效果
![](https://i.imgur.com/IhP7xoN.png)

### utilities
- 有一些tailwind沒有的效果，可以在tailwind.config.js中的plugin設定，亦可在tailwind.css中設定。

>tailwind.config.js
```bash=
const plugin = require("tailwindcss/plugin");
  plugins: [
  plugin(function({ addUtilities }) {
      const newUtilities = {
        //文字分散對齊
        ".text-dispersion": {
          textJustify: "inter-character",
          textAlignLast: "justify",
          textAlign: "text-justify"
        },
        //直向排列
        ".vertical": {
          writingMode: "vertical-rl"
        }
      };
      //*responsive，hover都加上自定義css
      addUtilities(newUtilities, ["responsive", "hover"]);
    })
  ]
};
```
### darkMode
- 在tailwind.config.js中設定，當`darkMode="class"`，class中只要有設定`dark:css效果`，就會顯示出dark模式的CSS效果，默認情況下，`darkMode=false`。

>tailwind.config.js
```bash=
darkMode: "class"
```

>App.vue
```bash=
<template>
  <div id="app" class="dark">
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  components: {
    HelloWorld
  }
};
</script>
```

>HelloWorld.vue
```bash=
<template>
  <div class="h-screen bg-gray-300">
    <p class="text-center text-white text-2xl dark:text-gray-900">Tailwind css</p>
    <div class="bg-green-50 flex flex-col justify-center items-center py-2">
      <button
        class="bg-blue-400  dark:bg-red-400 text-purple-100 rounded-lg px-4 py-2  hover:bg-blue-800 "
      >
        我是按鈕
      </button>
      <p class="font-light dark:text-red-500">我是一段文字</p>
    </div>
  </div>
  </template>
```
> 效果
- 沒有設置dark
    - ![](https://i.imgur.com/Cg1thPG.png)

- `class="dark"`
    - ![](https://i.imgur.com/kYL6iQ9.png)
