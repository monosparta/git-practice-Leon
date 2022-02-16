![git](https://i.imgur.com/1irVlrN.png)

### git的歷史及緣由

---

##### git   是一個分散式版本控制軟體
##### 最早由一位芬蘭的工程師創作
##### 2005年已開放原始碼的方式釋出
##### 開放原始碼的原因是開發者與相關Linux社群的主張
##### 為了替代專有軟體( BitKeeper )及效能不佳的( Monotone )
##### 所以git版本控制軟體就此誕生

### git常用指令集介紹

---

<font size="3" color="#000094"># SSH Key</font>
+ `$ ssh-keygen`
產生金鑰
+ `$ ls -al ~/.ssh`
查詢是否有 SSH Key
+ `$ pbcopy < ~/.ssh/id_rsa.pub` / `$ clip < ~/.ssh/id_rsa.pub`
複製公鑰 ( Mac / Windows )

<font size="3" color="#000094"># Config</font>
+ `git config --list`
查看設定	
+ `git config --local user.name "(userName)"	`
設定帳號
+ `git config --local user.email "(e-mail)"`
設定E-mail

<font size="3" color="#000094"># init / clone</font>
+ `git clone`
抓遠端儲存庫下來
+ `git init`
Git 初始化
+ `rm -rf .git`
移除 Git

<font size="3" color="#000094"># 基本版更</font>
+ `git status`
顯示修改檔案清單
+ `git add (file)`
添加檔案到索引
+ `git commit -m'message'`
提交添加到索引的檔案
+ `git push (remote) (branch)`
添加遠端數據庫
+ `git pull`
下載同步更新

<font size="3" color="#000094"># 分支與合併</font>
+ `git branch`
查詢所有本地分支
+ `git branch (newBranch)`
當前 commit 新建分支
+ `git checkout (branch)`
切換到某分支
+ `git branch -d (branch)`
刪除某分支
+ `git merge (branch)`
合併分支(平行)
+ `git merge --abort`
取消 merge