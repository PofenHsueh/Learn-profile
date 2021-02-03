# Git
## 基本概念
### Git是什麼
- Git是一種分散式版本的版本控制系統
>可以清楚紀錄每個檔案在什麼時候加進來、什麼時候被修改或刪除。
### Git不等於Github
- Git是一款版本控制軟體，而Github是一個商業網站，Github本體是一個Git伺服器。
### .gitignore檔案
- 有些檔案不想被git追蹤，在專案目錄新增一個`.gitignore`檔案，並設定想要忽略的規則。
    - `$ touch .gitignore`建立檔案
    - ![](https://i.imgur.com/PLho5Ww.png)
- `.gitignore`檔案設定的規則，只**對在規則設定之後的有效**。
### 不想再被Git控制版本
- Git的版控就是只靠`.git`目錄在做事，所以如果這個目錄不想被版控，只要將`.git`目錄移除，Git就對這個目錄失去控制權。
> 在整個專案目錄裡，什麼檔案目錄都可以救，但是只要刪除`.git`目錄，就救不回來了。
### 指令縮寫設定
- 將`$ git checkout`簡寫成`$ git co`：`$ git config --global alias.co checkout`
>設定之後，輸入`$ git co` 就跟`$ git checkout`會有一樣的效果。
###  command line基本指令（IOS）
- `ls`
    - 列出所有檔案和路徑 
    - 變化型
        - 列出隱藏的目錄：`ls -a`
        - 列出詳細資料：`ls -l`
        - 包上述兩個：`ls -la`
        - 列出 `.js` 的檔案：`ls *.js`
- `cd`
    - 切換目錄
    - 寫法： `cd 子目錄`
    - 變化型
        - 回到 home 目錄：`cd ~`
        - 回到根目錄：`cd /` 
        - 回到上一層資料夾：`cd ..`
    - 小技巧
        - 當輸入 cd 空格 時，按 tab 會幫你自動列出底下的資料夾列表。
        - 輸入前幾個字母，再按一次 tab 會幫你自動補完資料夾名稱。
- `clear` 
    - 清空 Terminal 面板 
- `pwd`
    - 目前路徑
- `mkdir`
    - 創建資料夾
    - 寫法：`mkdir 資料夾名稱`
- `rm` 
    - 刪除檔案，這邊的刪除檔案是「直接刪除」，並不會進到垃圾桶中，因此使用時要小心。
    - 變化型：
        - `rmdir`：刪除空資料夾，若資料夾內有檔案就無法刪除。
        - `rm -rf` ：刪除整個檔案或整個資料夾。
## 基本設定
### 安裝
- 安裝Homebrew
    - `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
- 安裝git
    - `$ brew install git`
- 確認是否成功
    - `$ git --version` 
### 識別資料
- 查看
    - `$ git config --list`
- 設定識別資料 
    - `$ git config --global user.name "Jade Hsueh"`
    - `$ git config --global user.email "jadeHsueh@example.com"`
### 設定SSH Key
- 檢查是否存在
    - `$ cd ~/.ssh`
    - `$ ls`
    - ![](https://i.imgur.com/Agl6Akh.png)
- 產生SSH Key
    - `$ ssh-keygen` 
- 打開SSH Key 
    - `$ cat ~/.ssh/id_rsa.pub` 
- 複製你的SSH Key到github or gitlab SSH Key設定裡。
## 常用指令
![](https://i.imgur.com/Zm8O3TF.png)
### 初始化數據庫：`$ git init`
- 讓Git開始對這個目錄進行版控。
>會在目錄裡建立一個`.git`目錄 （在一些作業系統是隱藏，要開啟檢視隱藏檔設定才能看到）
### 查詢當前狀態：`$ git status`
### 將檔案加入到索引：`$ git add '檔案名稱'`
- 讓Git開始追蹤它 
- 將全部加入追蹤`$ git add .` or `$ git add --all`
> `$ git add .`在舊版本中，這個指令會把「新增的檔案」以及「修改過的檔案」加到索引，但不會處理「刪除檔案」的行為，但在版本2.X之後就沒有這個問題。

> 雖然更新到2.X版後可以處理「刪除檔案」的行為，但是`$ git add .`這個指令會把目前當下這個目錄，以及子目錄裡的異動全部加到索引，但是，在這個目錄以外就不處理了（`$ git add --all`就沒這問題，不管在哪層都可以將檔案全部加入索引），所以執行這個指令要**注意自己所在的目錄位置**。
### 將索引檔案變成一個更新(commit)：`$ git commit -m "新增網頁環境"` 
- Git每次的commit只會處理索引（`$ git add .`）的內容，沒有加到索引就執行`git commit`的話，檔案會被無視。
#### Commit訊息很重要
- Git的commit訊息是要告訴自己或者其他人，**做了什麼修改**，像是"fix bug"這個commit就不適合，這樣其他人會不清楚這個commit是「修改什麼」。
- 英文、中文都可以，簡單清楚即可。
#### 修改commit紀錄
有下列幾種方法可以修改commit紀錄：
- `$ git rebase`
- `$ git reset`
- `--amend`
    - 只能修改最後一筆commit紀錄：`$ git commit --amend -m"your commit" `
    - 追加檔案到最後一筆commit紀錄：
        - `$ git add .` 
        - `$ git commit --amend --no-edit` 
### 查詢紀錄 `$ git log`
- 越新的資訊會在越上面
- 檢視單一檔案紀錄：`$ git log 檔案名稱`
### 刪除檔案 `$ git rm index.html`
- 執行`$ git rm index.html`是會將檔案刪除，若沒有真的要將檔案刪除，只是不想被Git控管
    - 加上 --cached參數：`$ git rm index.html --cached`
    - 要讓檔案再次被追蹤：`$ git add .`
### 切換分支：`$ git checkout`
- `$ git checkout 分支名稱`：切換到指定分支。
- `$ git checkout 檔名or路徑`：把檔案從.git目錄裡拉一份到目前的工作目錄。
### 還原版本：`$ git reset`
![](https://i.imgur.com/Oo4cPBu.png)
- 拆掉最後一次commit（練習reset指令）：
    - `$ git reset d458993^ `
>`^`符號代表「前一次」的意思，所以上面的指令指的是d458993這個commit的前一次，如果要往前5個紀錄，不會寫成d458993^^^^^，會寫成d458993~5。

>在這個例子中，HEAD跟dev都指向d458993這個commit，所以也可以寫成`$ git reset HEAD^` or `$ git reset dev^`。

>如果你確定你要回到18efe41（修改commit訊息）這個commit，就直接 `$ git reset 18efe41`。

- reset模式：
    - mixed 模式： 
        - `--mixed` 是預設的參數，如果沒有特別加參數，`$ git reset`指令將會使用 `--mixed` 模式。這個模式會把索引的檔案丟掉，但不會動到工作目錄的檔案，也就是說 Commit 拆出來的檔案會留在工作目錄，但不會留在索引。
    - soft 模式：
        - 這個模式下的reset，工作目錄跟索引的檔案都不會被丟掉，所以看起來就只有 HEAD 的移動而已。也因此，Commit拆出來的檔案會直接放在索引。
    - hard 模式：
        - 在這個模式下，不管是工作目錄以及索引的檔案都會丟掉。

|        模式        | mixed 模式（預設） | soft 模式  | hard 模式 |
|:------------------:|:------------------:|:----------:|:---------:|
| Commit拆出來的檔案 |    丟回工作目錄    | 丟回暫存區 | 直接丟掉  |

### `$ git fetch`
### `$ git pull`
### `$ git push`




<!-- Blob、Tree、Commit、Tag -->
