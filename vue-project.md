# Vue Project 以及 Vscode Debugger tool

Vue 在[官網中][vue]有提到 ***3*** 種如何使用 Debugger 工具來開發專案

* 使用 Debugger for Browser
* 使用官方的 Vue.js devtools
* 使用 js 原生的 debugger 關鍵字

## 使用 Debugger for Browser

---

此方法是使用 vscode 代理瀏覽器的 debugger 工具  

### 安裝 Vscode 插件

基本上各家瀏覽器 Firefox, Chrome 有推出相關的 Debugger 工具  
Vscode 安裝的部分特別沒有細部設定，查找後安裝即可

> 官方連結: [Firefox][firefox-debugger], [Chrome][chrome-debugger]  
> Edge 的設定官網沒有提及，有興趣自行研究

### 相關前置設定

依照官網中的提示，使用瀏覽器 debugger tool 需要確認

* 設定 webpack 使用 source-map \( firefox 為必要條件 \)
    1. 在 vue.config.js 中加入

        ```js
        module.exports = {
          configureWebpack: {
            devtool: 'source-map'
          }
        }
        ```

    1. 可以使用 vue inspect 確認該設定無誤

* vscode debugger 啟動設定
    1. 從 vscode 點選 `Run and Debug`  
    或在專案資料夾下建立`.vscode`資料夾以及`launch.json`檔

    1. 在 launch.json 中填入[官方提供][vue]的 debugger 設定  
    該 port 預設在 8080，請依照專案設定的 devServer port 做更改

        ```json
        {
          "version": "0.2.0",
          "configurations": [
            {
              "type": "chrome",
              "request": "launch",
              "name": "vuejs: chrome",
              "url": "http://localhost:8080",
              "webRoot": "${workspaceFolder}/src",
              "breakOnLoad": true,
              "sourceMapPathOverrides": {
                "webpack:///src/*": "${webRoot}/*"
              }
            },
            {
              "type": "firefox",
              "request": "launch",
              "name": "vuejs: firefox",
              "url": "http://localhost:8080",
              "webRoot": "${workspaceFolder}/src",
              "pathMappings": [{ "url": "webpack:///src/", "path": "${webRoot}/" }]
            }
          ]
        }
        ```

### debugger for browser 使用步驟

1. `npm run serve` 啟動專案
1. 啟動 `vuejs: chrome` 或 `vuejs: firefox`
1. 在專案中設置斷點 \( **break point** \)，檢查斷點是否觸發

## 使用 Vue.js devtools

---

Vue 官方提供相關的 debug 用瀏覽器插件  
該插件支援 vuex, vue router 等官方提供的功能

### 瀏覽器安裝插件

Firefox, Chrome 瀏覽器插件的安裝查找 `Vue.js devtool` 並安裝即可

> 官方連結: [Firefox][firefox-vue-extension], [Chrome][chrome-vue-extension]

### 使用方式

1. `npm run serve` 啟動專案
1. 使用安裝插件的瀏覽器訪問頁面
1. 開啟開發者工具\(F12\)並跳至 vue 選單

### 常用功能

1. 在選單中點及 vue component 後會將其掛載至 $vm0，在 console 選單即可直接操作
1. vuex 的撰寫格式若符合官方規範，該插件提供完整的 log 描述對於 store 狀態的更動

## 使用 js debugger

---

js 原生的 `debugger` 語句用法跟 `console.log(..)` 幾乎相同，
瀏覽器會在遇到 `debugger` 時中斷

> debugger 在 IE 瀏覽器中也支援

<!-- Links -->
[vue]:<https://vuejs.org/v2/cookbook/debugging-in-vscode.html>
[firefox-debugger]:<https://marketplace.visualstudio.com/items?itemName=firefox-devtools.vscode-firefox-debug>
[chrome-debugger]:<https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome>
[firefox-vue-extension]: <https://addons.mozilla.org/zh-TW/firefox/addon/vue-js-devtools>
[chrome-vue-extension]: <https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd>
