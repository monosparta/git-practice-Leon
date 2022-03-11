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


### .gitignore常用配置

---

+ `/floder/` 忽略整個floder資料夾
+ `*.zip` 忽略所有.zip文件
+ ` /floder/file.txt` 忽略folder下的file.txt文件
+ `fd/*` 忽略目錄fd下的全部內容
+ `!/fd2/bin/` 不忽略根目錄下的/fd2/bin/目錄

### 分支的使用方法


---

##### 為了將流程中不同的修改記錄的分開儲存，所以使用分支
##### 可讓分開的分支不受其他分支的影響
##### 因此在同一個工作流程裡可以同時進行多個不同的修改

#### 1.事前準備
##### 初始化資料夾
`$ git init`

##### 資料夾下建立`file.txt`的檔案，並且提交
>`file.txt`<br> git 分支的使用方法

##### 提交
`$ git add file.txt`
`$ git commit -m "first commit"`

#### 2.建立分支
##### 建立名為issue1的分支
`$ git branch issue1`
###### 功能或版本上的新增、修改都可以用分支的方式獨立作業，開發完整時再將分支合併回主幹

##### 若直接執行branch則可顯示列表，*號則是目前位於的分支
>`$ git branch`<br>issue1<br>*master
#### 3.切換分支
##### 切換到 issue1 分支
`$ git checkout issue1`
###### 若要在新建的分支上提交，則需要切換到該分支

##### 新增`file.txt`的檔案內容，並且提交，此時紀錄會在issue1分支上
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支
##### 提交
`$ git add file.txt`
`$ git commit -m "first commit"`
#### 4.合併分支
##### 切回master主幹
`$ git checkout master`
##### 此時master下的`file.txt`不會出現issue1分支的變更
>`file.txt`<br> git 分支的使用方法
##### 合併 issue1 分支
`$ git merge issue1`
###### 確認修改內容完整後即可將分支併回主幹

##### 執行合併後 分支的更動都會加回主幹
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支
#### 5.刪除分支
##### 執行以下命令
`$ git branch -d issue1`
##### 確認分支是否已被刪除
>`$ git branch`<br>*master
#### 6.平行操作
##### 建立兩個分支 並且切換到issue2
`$ git branch issue2`
`$ git branch issue3`
`$ git checkout issue2`
##### 在`myfile.txt`檔案增加文字然後提交
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br> commit 紀錄索引
##### 切換到issue3
`$ git branch issue3`
##### 剛剛新增的文字是在issue2增加的，所以issue3中不會出現
##### 新增以下文字
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br>pull 取得遠端數據庫
##### 這樣分別兩個在不同的分支平行增加了兩行不一樣的文字內容
#### 7.解決合併的衝突
##### 把issue2分支和issue3分支的修改合併到 master
##### 切換到master分支後，合併issue2分支
`$ git checkout master`
`$ git merge issue2`
##### 接著合併issue3
`$ git merge issue3`
##### 因在同一行文字進行修改，所以產生衝突。這時`myfile.txt`的內容如下：
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br>\<<<<<<< HEAD<br>commit 紀錄索引<br>\=======<br>pull 取得遠端數據庫<br>\>>>>>>> issue3
##### 找到差異的部分，做以下的修改
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br>commit 記錄索引的狀態<br>pull 取得遠端數據庫
##### 解決衝突後即可提交
`$ git add file.txt`
`$ git commit -m "merge issue3"`



---

##### 為了將流程中不同的修改記錄的分開儲存，所以使用分支
##### 可讓分開的分支不受其他分支的影響
##### 因此在同一個工作流程裡可以同時進行多個不同的修改

#### 1.事前準備
##### 初始化資料夾
`$ git init`

##### 資料夾下建立`file.txt`的檔案，並且提交
>`file.txt`<br> git 分支的使用方法

##### 提交
`$ git add file.txt`
`$ git commit -m "first commit"`

#### 2.建立分支
##### 建立名為issue1的分支
`$ git branch issue1`
###### 功能或版本上的新增、修改都可以用分支的方式獨立作業，開發完整時再將分支合併回主幹

##### 若直接執行branch則可顯示列表，*號則是目前位於的分支
>`$ git branch`<br>issue1<br>*master
#### 3.切換分支
##### 切換到 issue1 分支
`$ git checkout issue1`
###### 若要在新建的分支上提交，則需要切換到該分支

##### 新增`file.txt`的檔案內容，並且提交，此時紀錄會在issue1分支上
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支
##### 提交
`$ git add file.txt`
`$ git commit -m "first commit"`
#### 4.合併分支
##### 切回master主幹
`$ git checkout master`
##### 此時master下的`file.txt`不會出現issue1分支的變更
>`file.txt`<br> git 分支的使用方法
##### 合併 issue1 分支
`$ git merge issue1`
###### 確認修改內容完整後即可將分支併回主幹

##### 執行合併後 分支的更動都會加回主幹
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支
#### 5.刪除分支
##### 執行以下命令
`$ git branch -d issue1`
##### 確認分支是否已被刪除
>`$ git branch`<br>*master
#### 6.平行操作
##### 建立兩個分支 並且切換到issue2
`$ git branch issue2`
`$ git branch issue3`
`$ git checkout issue2`
##### 在`myfile.txt`檔案增加文字然後提交
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br> commit 紀錄索引
##### 切換到issue3
`$ git branch issue3`
##### 剛剛新增的文字是在issue2增加的，所以issue3中不會出現
##### 新增以下文字
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br>pull 取得遠端數據庫
##### 這樣分別兩個在不同的分支平行增加了兩行不一樣的文字內容
#### 7.解決合併的衝突
##### 把issue2分支和issue3分支的修改合併到 master
##### 切換到master分支後，合併issue2分支
`$ git checkout master`
`$ git merge issue2`
##### 接著合併issue3
`$ git merge issue3`
##### 因在同一行文字進行修改，所以產生衝突。這時`myfile.txt`的內容如下：
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br>\<<<<<<< HEAD<br>commit 紀錄索引<br>\=======<br>pull 取得遠端數據庫<br>\>>>>>>> issue3
##### 找到差異的部分，做以下的修改
>`file.txt`<br>git 分支的使用方法<br>checkout 切換分支<br>commit 記錄索引的狀態<br>pull 取得遠端數據庫
##### 解決衝突後即可提交
`$ git add file.txt`
`$ git commit -m "merge issue3"`

### Commit 介紹及使用

---

##### 開發者要將修改檔案後的專案內容，增加為一個新的專案版本，這個動作就稱為提交(`Commit`)
##### 開發者可以每開發完一項功能，或一個版本，就先將程式碼`commit`到本機端儲存庫上，等到多次提交後，再一次將本機端儲存庫上的專案程式碼，一次性發布(`Push`)到GitHub網站上的雲端儲存庫
#### 使用方式
###### 使用`commit`前，必須將欲提交的檔案以`add`指令追蹤該檔案
##### 以index.html為例
`$ git add index.html`
##### 提交index.html
`$ git commit -m "message"`
##### index.html檔案即儲存到本地數據庫，"message"可自行設定版本資訊或文字說明
##### 其他相關參數
##### 所有修改的檔案都 commit，但是 untracked file 還是得要先 add
`$ git commit -a`
##### 加入比對結果
`$ git commit -v`
##### 修改前一次提交 (追加檔案到最近一次的 Commit)
`$ git commit --amend`

### GitHub 使用方法：push, pull 實作

---

#### push

![mono](https://imgur.com/X7O8www.png)

##### 右下角`New`建立新的專案

![repository](https://imgur.com/0tbr01y.png)

##### `Create repository`點下去
##### 遠端數據庫就創建完成了
##### 接著要把本地數據上傳到遠端
##### 首先先添加遠端數據庫

![code](https://imgur.com/U2iEyKl.png)

##### `Code`中可看到遠端數據庫的位置
##### 接著就可以在終端機輸入

`$ git remote add origin https://github.com/monosparta/git-practice-Leon.git`

##### 並且`push`本地檔案到遠端
`$ git push origin master`

##### 檔案就會出現在遠端上啦!
![git.md](https://imgur.com/Emq27CM.png)

#### pull

##### 如果在遠端數據庫修改檔案，pull指令可以將其合併到本地端
##### `pull.md`遠端內容

![pull](https://imgur.com/aruZcVC.png)

##### 新增內容後按下`commit changes`

![add text](https://imgur.com/wICZ2aI.png)

##### 本地的`pull.md`內容
![local](https://imgur.com/vGMq2wZ.png)

##### 執行`pull`指令

`$ git pull origin master`

![cmd](https://imgur.com/1UxC9gx.png)

##### 再回到`pull.md`檔案發現內容已經被抓下來了~

![local2](https://imgur.com/2Mbl8WX.png)

### GitFlow 介紹

---

##### 當專案的開發人員越來越多，如果沒有訂規矩，每個人習慣不同，在Commit上可能會出大亂
##### GitFlow 是最早出現的一套流程，且廣泛被應用
##### GitFlow 提出不同的分支功能建議，分別有 `master`、`develop` 、`hotfix`、`release`、`feature` 五種分支

#### 長期分支
##### `master`分支、`develop`分支
###### 會一直存活在整個 Git flow 裡，並不會被刪除掉
#### 短期分支
##### `hotfix`分支、`release` 分支、`feature` 分支
###### 當完成專案後，這些更新的版本都會被合併進 Master 或 Develop 分支 ，之後就會被刪除掉
#### 分支說明
##### `master`分支
##### master 是當 Git 建立版本控制時，就預設的分支，主要用來放穩定、隨時可上線的版本
- 永遠處在 production-ready 狀態
- 來源是從其他分支合併過來，開發者不會直接 Commit 到此分支上
- 因為是穩定版本，所以通常會在 `master` 分支上的 Commit 貼上「 版本標籤 」
##### `develop`分支
##### 作為主要開發的分支，是所有短期分支的基礎分支
- 最新的下次發佈開發狀態
- `feature` 分支從 `develop` 分支切出去，當功能完成後，在合併回來 `develop` 分支
##### `hotfix`分支
##### 主要功能是用來進行修復
- 從 `master` 分支切出來的
- 當修復完後，會合併回 `master` 分支， 也同時會合併回 `develop` 分支
##### `release`分支
##### 在 Develop 分支發布正式版本到 Master 分支之前，可以先進行一個預備發布的本版本進行測試
- 從 `develop` 分支切出來
- 完成後需合併到 `master` 分支與 `develop` 分支

##### `feature`分支
##### 主要用來新增功能的分支
- 都是從 `develop` 分支切出來的，完成後再合併回 `develop` 分支
#### Github flow
##### GitFlow的簡化版
##### 只有一個長期分支 - `master`分支
##### 流程
1. 根據需求，從 `master` 分支切出其他分支進行開發。
2. 開發完成或是需要討論時，向 `master` 分支發起 pull request 請求
3. Pull request 請求被接受後，合併到 `master` ，重新部署後，原先的分支則被刪除
#### Gitlab flow
##### GitFlow 與 GitHub flow 的合併模式流程
##### 原則
- 以「上游優先」（upsteam first）。意指只認存在一個主要分支 `master` 分支，他是其他所有分支的「上游」。只有這隻上游分支採納的代碼變化，才能應用到其他分支
##### 針對不同開發的情況
1. 「持續發布」- 除了 `master` 分支外，根據不同環境建立對應的分支。並需服從上游到下游一層一層的過關規則
2. 「版本發佈」- 每當有一個穩定的版本，就要從 `master` 分支拉出一個分支。只有修補 Bug 時，才允許將代碼合併到這些分支，並且需要更新小版本號
