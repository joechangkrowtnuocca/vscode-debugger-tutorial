# Java Project 以及 Vscode Debugger Tool

## 安裝插件

---

在 Vscode 開發 java 專案，請先下載插件包 `java extension pack`
> 官網連結: [java extension pack][java-extension-pack]  
> 該插件目前使用版本為 jdk 11

## 範例講解

---

* 建立一個 groupId 為 foo.bar 以及 artifactId 為 sample 的 spring boot 專案
* 開啟專案後，在 vscode 左邊的 activity bar 中點擊 `RUN` 當中的 `create a launch.json file`
* 在專案資料夾下，建立`.vscode`資料夾以及`launch.json`，使用第 2 組設定啟動

  > 注意一下，第一組設定雖為在各自的 java 檔中啟動 main 方法，若引用到 spring 物件時，並不會自動引入。
    建議撰寫 unit test code 做為各自 java 檔的測試

    ```json
    {
      // Use IntelliSense to learn about possible attributes.
      // Hover to view descriptions of existing attributes.
      // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
      "version": "0.2.0",
      "configurations": [
        {
          "type": "java",
          "name": "Launch Current File",
          "request": "launch",
          "mainClass": "${file}"
        },
        {
          "type": "java",
          "name": "Launch SampleApplication",
          "request": "launch",
          "mainClass": "foo.bar.sample.SampleApplication",
          "projectName": "sample"
        }
      ]
    }

    ```

<!-- links -->
[java-extension-pack]:<https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack>
