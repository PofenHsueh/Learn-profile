# Git
## Git是什麼
- Git是一種分散式版本的版本控制系統
>可以清楚紀錄每個檔案在什麼時候加進來、什麼時候被修改或刪除。
- **Git不等於Github**
    - Git是一款版本控制軟體，而Github是一個商業網站，Github本體是一個Git伺服器。
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
## 基本概念
### .gitignore檔案
- 有些檔案不想被git追蹤，在專案目錄新增一個`.gitignore`檔案，並設定想要忽略的規則。
    - `$ touch .gitignore`建立檔案
    - ![](https://i.imgur.com/PLho5Ww.png)
- `.gitignore`檔案設定的規則，只**對在規則設定之後的有效**。
### 不想再被Git控制版本
- Git的版控就是只靠`.git`目錄在做事，所以如果這個目錄不想被版控，只要將`.git`目錄移除，Git就對這個目錄失去控制權。
> 在整個專案目錄裡，什麼檔案目錄都可以救，但是只要刪除`.git`目錄，就救不回來了。
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
### 刪除檔案 `$ git rm `
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

### 開始使用分支：`$ git branch`
- 查看所有分支： `$ git branch -a`
- 新增分支：`$ git branch 「新分支名稱」`
- 更改分支名稱： `$ git branch -m 「舊分支名稱」「新分支名稱」`
- 刪除分支： `$ git branch -d 「分支名稱」`

### 取得遠端數據庫的最新歷史記錄：`$ git fetch`
### 合併分支：`$ git merge`
- 不要使用快轉模式合併：`$ git merge 「分支名稱」 --no-ff`
### 下載更新：`$ git pull`
- git pull = git fetch+git merge
- 不要額外的commit：`$ git pull --rebase`
- pull完產生衝突，解完衝突後，將剛剛的東西`$ git add .`進去索引區，再執行`$ git rebase --continue`就不會而外新增一個commit訊息。
### 新增遠端版本庫： `$ git remote`
- $ git remote add origin 「GitHub Respository位置」。
    - add指令是指要加入一個遠端的節點。
    - 在這裡的origin是一個代名詞，指的是後面那串GitHub伺服器的位置。 
    - 遠端的節點預設就會叫origin。
### 將檔案上傳至遠端：`$ git push`
- `$ git push -u origin master`
    - master這個分支的內容，推向 origin這個位置。
    - 在 origin 那個遠端 Server 上，如果 master 不存在，就建立一個叫做 master 的同名分支。
    - 但如果本來 Server 上就存在 master 分支，便會移動 Server上 master分支的位置，使它指到目前最新的進度上。
    - 設定 upstream，就是那個` -u `參數
        - 如果有設定，當下次執行 git push 指令的時候，它就會用來當預設值（以上述為例：預設為origin的master分支）。
        - 沒設定，就必須在每次 Push 的時候都跟 Git 講清楚、說明白：`$ git push origin master`。

### 將檔案從遠端複製到本地：`$ git clone`
- `$ git clone 「Repository的SSH或HTTPS」`
- Clone 指令會把整個專案的內容複製一份到你的電腦裡，這裡指的「內容」不是只有檔案，而是指所有整個專案的歷史紀錄、分支、標籤等內容都會複製一份下來。
### 指令縮寫設定：`$ git config --global alias.簡寫 指令名稱`
- `$ git config --global alias.co checkout`將`$ git checkout`簡寫成`$ git co`
>設定之後，輸入`$ git co` 就跟`$ git checkout`會有一樣的效果。
## 進階概念
### HEAD是什麼？
- HEAD是一個指標，指向某一個分支，通常可以把HEAD當作「目前所在分支」，但當HEAD沒有指向某個分支時會造成「detached HEAD」（斷頭）。 
### SHA-1值
- 圖中紅框為SHA-1（Secure Hash Algorithm 1），是一種雜湊演算法，計算之後的結果通常會以40個十六進位的數字呈現。
- Git裡所有物件的「編號」的計算主要都是靠這個演算法產生。
- 特點：
    - 輸入一樣的值，會有相同的輸出值。 
![](https://i.imgur.com/sy9zPz2.png)
- 在Git裡，不同種類的SHA-1值計算會稍微有些不同，舉例來說，Blob物件的SHA-1計算公式是：
    1. "blob"字樣
    2. 一個空白字元
    3. 輸入內容的長度
    4. Null結束符號
    5. 輸入內容
> 如果是Tree物件，第一項則改為"tree";如果是Commit 物件，第一項則改為"commit"，以此類推。 
- Git內建hash-object指令計算SHA-1值
    - `$ printf "Hello git test" | git hash-object --stdin`
![](https://i.imgur.com/t0JXMEB.png)

### .git目錄有什麼
- 打開隱藏的.git檔
    - mac
        - `command+shift+.`
    - [windows](https://helpx.adobe.com/tw/x-productkb/global/show-hidden-files-folders-extensions.html)
- Git裡的四種物件:
    - Blob物件
    - Tree物件
    - Commit物件
    - Tag物件 
#### Blob物件
先建立一個檔案"index.html"，內容為"Blob objects"字串，在使用`$ git add index.html` 加到Git的索引區。
- **Blob物件是用來存放index.html這個檔案的「內容」。**
- 使用`$ git add ` 將檔案加入至索引區，Git會根據這個物件的「內容」計算出SHA-1值。
- Git接著會用這個SHA-1值的前兩個字當作目錄內容，後38個字當作檔案名稱，把目錄及檔案建立並存放在 .git/object目錄下。
- 這個檔案的內容則是Git使用壓縮演算法，把原本的「內容」壓縮之後的結果。
![](https://i.imgur.com/CnEBxh8.png)
>Blob物件的檔名是由SHA-1演算法決定，Blob的內容由壓縮演算法決定。
#### Tree物件
進行 `$ git commit -m "init commit"` 會發現.git/objects裡的檔案多出了2個資料夾。
![](https://i.imgur.com/pTHzjJg.png)
使用 `$ git cat-file -t 「SHA-1值」`，看看這個物件是什麼東西，會看到一個寫tree，一個寫commit。
![](https://i.imgur.com/DQkjI61.png)
使用 `$ git cat-file -p 「SHA-1值」` ，查看Tree物件的內容，在這個Tree物件裡看到一個Blob物件，正是剛剛放在目錄裡的index.html
![](https://i.imgur.com/HY2mjUZ.png)
- 檔案在Git裡會以Blob物件方式存放，ex.上述的index.html。
- 目錄以及檔案的名，將以Tree物件的方式存。
- **Tree物件的內容會指向某個或某些Blob物件，或是其他的Tree物件。**
#### Commit
還記得在commit後，所多出來的東西，一個是tree一個是commit，剛剛提到了tree，接下來就要提到另一部份「commit」。
使用 `$ git cat-file -p 「SHA-1值」`查看Commit物件的內容，看看這個Commit物件的內容：
![](https://i.imgur.com/bRqqwUk.png)
- **Commit物件會指向某個Tree物件。**
- **Tree物件的內容會指向某個或某些Blob物件，或是其他的Tree物件。**
![](https://i.imgur.com/fZ0RfGM.png)

#### Tag
- 在開發軟體有完成特定的里程碑，例如：軟體版號1.0.0或者bata-release。
- 標籤有2種，都可以把它當作貼紙一樣看待：
    - **輕量標籤（lightweight tag）**：
        - 直接指定打算貼上去的Commit。
        - 指向某個Commit的指標，沒有含其他資訊。
        - `$ git tag 標籤名 SHA-1值(6碼) `
        - ![](https://i.imgur.com/V3pKBDX.png)
    - **附註標籤（annotated tag）**： 
        - `$ git tag 標籤名 SHA-1值(6碼) -a -m "tag info"`
            - `-a`參數就是請Git幫你建立有附註的標籤，而後面的`-m`則是跟我們在做一般commit一樣輸入訊息，沒有`-m`則會進入Vim編輯器（編輯按`i`，結束編輯按`esc`+`:` `wq`）。 
        - 附註標籤的好處就是有更多關於這個標籤的資訊
            - `$ git show 標籤名` 
            - ![](https://i.imgur.com/QohVdtq.png)

- 刪除標籤：
    - `$ git tag -d 標籤名 ` 

#### 四種物件的關係
![](https://i.imgur.com/V62su91.png)
- 檔案加入Git後，檔案的內容會被轉成Blob物件儲存。
- 目錄及檔名會存放在Tree物件內，Tree物件會指向Blob物件，或是其他的Tree物件。
- Commit物件會指向某個Tree物件。除了第一個Ｃommit之外，其他的Commit都會指向前一次的Commit物件。
- Tag物件會指向某個Commit物件。
- **分支雖然不屬於這四個物件之一，但他會指向某個Commit物件。**
- **HEAD亦不屬於這四個物件，單他會指向某個分支。**
- 當開始往Git Server上推送之後，在.git/refs底下就會多出一個remote的目錄，裡面放的是遠端的分支基本上跟本地的分支是差不多的概念，同時也會指向某個Commit物件。
