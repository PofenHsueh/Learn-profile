# Vite
### vite（v特）是什麼
- 提供開發者快速啟動、即時更新的**開發工具**
- 安裝即使用，預設無設定檔
- 加速你的**開發體驗**，不加速你的應用效能
### 建立vite專案
```bash=
$ npm init vite-app <project-name>
$ cd <project-name>
$ npm install
$ npm run dev
```
OR
```bash=
$ yarn create vite-app <project-name>
$ cd <project-name>
$ yarn
$ yarn dev
```

### vite ＆ webpack比較
- webpack
    -  需要靜態分析過 app 的所有檔案以及套件的相依性，然後根據這些資訊把東西包在一起。
    -  component越多，花的時間越多。
![](https://i.imgur.com/nSUB3ZO.png)
- vite
    - vite不全部編譯、打包，直接 run dev，只編譯有更新的部分。
    - 用 WebSocket 將變更的component更新。
    - 預設不全部編譯，可以在 run dev 指令時用 `--force `option 強迫編譯。
    - - 預設產生的request較多。
![](https://i.imgur.com/Owah2Bl.png)

### vite運作原理
- ES Modules
    - ES6標準化模組
        - import
        - export
    - 瀏覽器支援還不夠完善
        - ![](https://i.imgur.com/uCmGrsF.png)
        - 加上type="module"，瀏覽器才看得懂
        - ![](https://i.imgur.com/57Kkp7j.png)
    - 必須是絕對或是相對路徑，才能讀取到該 module 
    - Node.js要直接使用ES modules，副檔名`.js-` -> `.mjs`

- 類似[Snowpack](https://www.snowpack.dev/)
    - ![](https://i.imgur.com/1BFm1VU.jpg)



##### 資料來源
- [webpack 新手教學之淺談模組化與 snowpack](https://blog.techbridge.cc/2020/01/22/webpack-%E6%96%B0%E6%89%8B%E6%95%99%E5%AD%B8%E4%B9%8B%E6%B7%BA%E8%AB%87%E6%A8%A1%E7%B5%84%E5%8C%96%E8%88%87-snowpack/)
- [Vite 怎麼能那麼快？從 ES modules 開始談起](https://blog.techbridge.cc/2020/08/07/vite-and-esmodules-snowpack/)
- [ES modules ](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)
- mopcon 2020

