![git](https://i.imgur.com/1irVlrN.png)

### git的歷史及緣由

---

##### git   是一個分散式版本控制軟體
##### 最早由一位芬蘭的工程師創作
##### 2005年已開放原始碼的方式釋出
##### 開放原始碼的原因是開發者與相關Linux社群的主張
##### 為了替代專有軟體( BitKeeper )及效能不佳的( Monotone )
##### 所以git版本控制軟體就此誕生

### 版本控制

---

##### 版本控制可協助追蹤在程式碼中的變更
##### 開發人員只要將每次程式碼的變更都紀錄起來
##### 就可以瀏覽所有開發的歷史紀錄
##### 掌握團隊的開發進度
##### 對程式碼作任何修改都可以輕易的復原回之前正常的版本
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

### 分支的使用方法

---

###### 為了將流程中不同的修改記錄的分開儲存，所以使用分支
###### 可讓分開的分支不受其他分支的影響
###### 因此在同一個工作流程裡可以同時進行多個不同的修改

#### 1.事前準備
###### 初始化資料夾
`$ git init`
###### 資料夾下建立`file.txt`的檔案，並且提交
>`file.txt`
> git 分支的使用方法

###### 提交
`$ git add file.txt`
`$ git commit -m "first commit"`

#### 2.建立分支
###### 建立名為issue1的分支
`$ git branch issue1`
<font size="1">*功能或版本上的新增、修改都可以用分支的方式獨立作業，開發完整時再將分支合併回主幹</font>

###### 若直接執行branch則可顯示列表，*號則是目前位於的分支
>`$ git branch`
>`issue1`
>`*master`
#### 3.切換分支
###### 切換到 issue1 分支
`$ git checkout issue1`
<font size="1">*若要在新建的分支上提交，則需要切換到該分支</font>

###### 新增`file.txt`的檔案內容，並且提交，此時紀錄會在issue1分支上
>`file.txt`
> git 分支的使用方法
> checkout 切換分支
###### 提交
`$ git add file.txt`
`$ git commit -m "first commit"`
#### 4.合併分支
###### 切回master主幹
`$ git checkout master`
###### 此時master下的`file.txt`不會出現issue1分支的變更
>`file.txt`
> git 分支的使用方法
###### 合併 issue1 分支
`$ git merge issue1`
<font size="1">*確認修改內容完整後即可將分支併回主幹</font>

###### 執行合併後 分支的更動都會加回主幹
>`file.txt`
> git 分支的使用方法
> checkout 切換分支
#### 5.刪除分支
###### 執行以下命令
`$ git branch -d issue1`
###### 確認分支是否已被刪除
>`$ git branch`
>`*master`
#### 6.平行操作
###### 建立兩個分支 並且切換到issue2
`$ git branch issue2`
`$ git branch issue3`
`$ git checkout issue2`
###### 在`myfile.txt`檔案增加文字然後提交
>`file.txt`
> git 分支的使用方法
> checkout 切換分支
> commit 紀錄索引
###### 切換到issue3
`$ git branch issue3`
###### 剛剛新增的文字是在issue2增加的，所以issue3中不會出現
###### 新增以下文字
>`file.txt`
> git 分支的使用方法
> checkout 切換分支
> pull 取得遠端數據庫
###### 這樣分別兩個在不同的分支平行增加了兩行不一樣的文字內容
#### 7.解決合併的衝突
###### 把issue2分支和issue3分支的修改合併到 master
###### 切換到master分支後，合併issue2分支
`$ git checkout master`
`$ git merge issue2`
###### 接著合併issue3
`$ git merge issue3`
###### 因在同一行文字進行修改，所以產生衝突。這時`myfile.txt`的內容如下：
>`file.txt`
> git 分支的使用方法
> checkout 切換分支
> \<<<<<<< HEAD
> commit 紀錄索引
> \=======
> pull 取得遠端數據庫
> \>>>>>>> issue3
###### 找到差異的部分，做以下的修改
>`file.txt`
> git 分支的使用方法
> checkout 切換分支
> commit 記錄索引的狀態
> pull 取得遠端數據庫
###### 解決衝突後即可提交
`$ git add file.txt`
`$ git commit -m "merge issue3"`