# Git
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
    - `$ git config --global user.email jadeHsueh@example.com`
### 設定SSH Key
- 檢查是否存在
    - `$ cd ~/.ssh`
    - `$ ls`
    - ![](https://i.imgur.com/Agl6Akh.png)
- 產生SSH Key
    - `$ ssh-keygen` 
- 打開SSH Key 
    - `$ cat ~/.ssh/id_rsa.pub` 
- 複製你的SSH Key到github or gitlab SSH Key設定裡

###  command line基本指令
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

### Git指令
![](https://i.imgur.com/Zm8O3TF.png)
- 初始化數據庫： `$ git init`
- 查詢當前狀態：`$ git status`
- 將檔案加入到索引：`$ git add .`
- 將索引檔案變成一個更新(commit)：`$ git commit -m "新增網頁環境"`

