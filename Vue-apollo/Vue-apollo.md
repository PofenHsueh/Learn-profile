# Vue-apollo
###### tags: `前端`
### Apollo Client
著重於從客戶端**向服務端發送和接收請求**。
所有的內容都是通過單個端點發送和接收的。
* Apollo Link處理網路請求。
* Apollo Cache處理緩存。
* Apollo Client緊接著將連接和緩存整合起來，高效地管理同GraphQL服務有交互。

### 安裝
以下有2種方式可進行安裝：
#### Vue CLI 插件
`vue add apollo`
#### 手動安裝
**1. Apollo Client**：利用Apollo工具建構GraphQL客戶端。
   * `npm install --save vue-apollo graphql apollo-boost`
     *  `graphql`它包含了GraphQL語言解析器。
     *  `apollo-boost`，它包含了創建Apollo Client和發送操作所必須的Apollo包。
     *  `vue-apollo`，它是包含了構建Apollo用戶介面的Vue組件。
   * `apollo-boost` 中的構造函數ApolloClient可用於創建我們的第一個客戶端，**通過ApolloClient構造函數創建了一個新的client實例。**
```bash=
import ApolloClient from 'apollo-boost'

const apolloClient = new ApolloClient({
  // 你需要在這裡使用絕對路徑
  uri: 'https://api.graphcms.com/simple/v1/awesomeTalksClone'
})
``` 
**2. 安装插件到 Vue**
```bash=
import Vue from 'vue'
import VueApollo from 'vue-apollo'

Vue.use(VueApollo)
```
**3. Apollo provider**
Provider 保存了可以在接下來被所有子組件使用的Apollo 客戶端實例。
```bash=
const apolloProvider = new VueApollo({
  defaultClient: apolloClient,
})
```
使用apolloProvider選項將它添加到你的應用程序:
```bash=
new Vue({
  el: '#app',
  // 像 vue-router 或 vuex 一樣引入 apolloProvider
  apolloProvider,
  render: h => h(App),
})
```
<!-- ## 實戰
- **建立資料夾，裡面會存放api的schema格式。**
    - ![](https://i.imgur.com/4Ek4yjG.png)
- **亦可直接將schema寫在需要呼叫的畫面裡。**
    - 缺點：使用相同api需要重複撰寫schema  -->

### 查詢（Query）
以下示範2種方法去做query，將api的schema放在資料夾中統一管理，若需呼叫相同api，不需重複撰寫schema（可避免眼殘看錯，程式碼看起來也比較乾淨）。
>schema/accList.js
- **資料夾統一管理api schema**
    - ![](https://i.imgur.com/4Ek4yjG.png)
    - import graphql tag
        - `import gql from 'graphql-tag'`
    - 按照playground的格式撰寫schema
        - playground：![](https://i.imgur.com/yiznYPT.png)
        - schema：![](https://i.imgur.com/7KIlSyU.png)

>（AccList.vue）
- 呼叫api
```bash=
import accList from "../schema/accList";
export default {
    apollo:{
        ACCList: {
          query: accList.ACC,
        },
    }
}
```


---


>（AccList.vue）
- **在component中直接寫schema**
 ```bash=
import gql from "graphql-tag";
export default {
    apollo:{
        ACCList: {
          query: gql`
            query ACCList {
              ACCList {
                hasMore
                cursor
                accs {
                  name
                  content {
                    cover
                    printMode
                    materials {
                      materialName
                      startPage
                      endPage
                    }
                  }
                }
              }
            }
          `
        }
    }
}
```
### 變異（Mutate）
>schema/signUp.js
- **資料夾統一管理api schema**
    - import graphql tag
        - `import gql from 'graphql-tag'`
    - 按照playground的格式撰寫schema
        - playground ![](https://i.imgur.com/yxNrTmv.png)
        - schema ![](https://i.imgur.com/u5NhuEV.png)
>SingUp.vue
```bash=
import { SIGN } from "../schema/signUp";
export default {
     data() {
        return {
          newAuthor: {
            userName: "",
            password: ""
          }
        };
      },
    async signUp() {
          const response = await this.$apollo.mutate({
            mutation: SIGN,
            variables: {
              userInfo: {
                userName: this.newAuthor.userName,
                password: this.newAuthor.password,
                roles: ["WORKER"]
              }
            }
          });
          console.log(response);
        }
    }
```
### 權限
練習vue-apollo的時候，遇到權限的問題，以下有2種方式可以解決（都是在vue.apollo.js中設定）：
1. vue-apollo.js中，裡面提供`getAuth`的function，只要在這邊設定token，就可以將token帶到header中，當發起請求，就會一起帶到後端。
    * ![](https://i.imgur.com/WET4JGe.png)
    
    * ![](https://i.imgur.com/caYksBt.png)

2. 使用setContext方法
    * `import { setContext } from "apollo-link-context";`

    * 宣告一個authLink，將token放入header中
        * ![](https://i.imgur.com/xHofLVA.png)
    * defaultOptions中設定link
        * ![](https://i.imgur.com/sa5B0aU.png)

    * api中的header中，帶有Bearer，此部分需注意
        * ![](https://i.imgur.com/YL7kOe7.png)


<!-- #### fetchPolicy apollo 选项
* cache-first：嘗試從緩存中首先讀取數據。如果查詢所需的數據都在緩存中，那麼將返回該數據。如果緩存結果不可用，Apollo將會從網絡中獲取。這個策略減少渲染組件時發送的網絡請求數量。

* cache-and-network：這會讓Apollo首先嘗試從緩存中讀取數據。如果完成查詢所需的所有數據都在緩存中，那麼將返回該數據。但是，無論整個數據是否在緩存中，這fetchPolicy將始終使用網絡接口執行查詢，cache-first而只有在數據不在緩存中時才會執行查詢。此策略讓用戶獲得快速響應進行了優化。

* network-only：這永遠不會從緩存中返回初始數據。相反，它將始終使用您的網絡接口向服務器發出請求。特性是與 Server 的數據一致性。

* cache-only：這永遠不會使用網絡查詢。相反，它從緩存讀取。如果數據不存在，則會拋出錯誤。 -->