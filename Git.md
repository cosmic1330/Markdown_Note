# Git 深入淺出
遠端版本庫是指被託管在網際網路或其他網路中的各種專案版本庫。與其它人協同工作包括了：「管理」遠端版本庫、以及將分享的資料「推送（push）」到端遠版本庫、或者從遠端版本庫「拉取（pull）」分享的資料。
- [Git中文文檔](https://git-scm.com/book/zh-tw/v2/Git-%E5%9F%BA%E7%A4%8E-%E8%88%87%E9%81%A0%E7%AB%AF%E5%8D%94%E5%90%8C%E5%B7%A5%E4%BD%9C)
- [Git指令集](https://backlog.com/git-tutorial/tw/reference/basic.html)

[img01]:/image/Git.png "git圖片"
![alt][img01]
## 前置準備
### 1.創建SSH密鑰
> 在終端機使用指令創建SSH密鑰，會在該目錄下產生 .ssh的資料夾 及兩個檔案(id_rsa.pub =>公鑰 、 id_rsa=>私鑰)
```go
$ ssh-keygen -t rsa -C  "john@example.com"
//rsa 為一種加密模式
```
### 2.將公鑰添加至git設定裡
> 打開.ssh資料夾 id_rsa.pub檔案，裡面加密後的為ssh金鑰
```go
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDOWols+uGuuYTPYucNI2TtAxDrJhwyOWDfQtHNeOsWLAoG/kZez3InFsSA1b/cOQEs616x0pcG5wydc06P~~~
```
將金鑰添加至Github的設定中
![ssh01](/image/ssh.png)
### 3.確認是否連線成功
> 在終端機輸入指令 $ssh -T git@github.com
- 第一次連線會請求創建known_hosts檔案
(有此檔案才可與git成功連結)
```go
$ssh -T git@github.com
//出現以下訊息表示連線成功
Hi cosmic1330! You've successfully authenticated, but GitHub does not provide shell access.
```
***
## 設定Git 識別資料
> Git 提交會使用指定使用者名稱及電子郵件帳號
- 若有指定 --global 參數，只需要做這工作一次。因為在此系統，不論 Git 做任何事都會採用此資訊。
- 若想指定不同的名字或電子郵件給特定的專案，只需要在該專案目錄內執行此命令，並確定未加上 --global 參數。
```go
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com


$ git config user.name "John Doe"
$ git config user.email johndoe@example.com
//設定此次提交的資訊
```
***
## 創建Git專案
## `下載Github上現有的專案`
> 在終端機上輸入git clone [url]
- 執行 clone 命令時，會自動設定遠端數據庫為追踪目標。這樣在 push 或 fetch/pull 命令時即使省略 repository，也可以正確的顯示/讀取修改內容。
```go
$git clone https://github.com/cosmic1330/web-interwiew

＊ $ git push <repository> <refspec>
//如果有使用clone，之後push時<repository>可省略
```
## `初始化一個Git數據庫`
> 如果專案是第一次創建，並非git clone的，需在資料夾內初始化git。
- 會在資料夾內創建 隱藏的.git檔案
```go
$git init
```
***
## 基本指令操作
### **1.查看git資料夾狀態**
> 在目錄內輸入 $git status
```go
$git status
//可檢視檔案狀態
$git diff
//可檢視尚未預存的修改內容差異
```
會出現資料夾內檔案狀態
```go
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   Css.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        Git.md
        Json.md
        image/Git.png
        image/json.png
        image/ssh.png
        image/webpack.png
        webpack.md

no changes added to commit (use "git add" and/or "git commit -a")
```
### **2.出現上列訊息 表示資料夾內有未追蹤或未預存的檔案**
> 輸入$git add [檔案名稱]，將檔案開始追蹤並加入預存
```go
$git add Css.md
```
### **3.提交變更**
> 提交 預存區的檔案
```go
$ git commit
$ git commit -m [本次提交的備註]
//未輸入-m則 會開啟提交訊息編輯器
$ git commit -a 
//略過預存區，略過 git add 步驟，-a會納入所有已變更的檔案
```
### **4.傳送至遠端版本庫**

```go
$git push [remote-name] [branch-name]
//例如:$ git push origin mas
```
### **`補充`**
1.刪除預存區的檔案
- **$git rm** 換句話說，你想保留在磁碟機上的檔案但不希望 Git 再繼續追蹤它。
- **$git reset** 將檔案剔除預存區。
> git rm 刪除後同時也會將該檔案從工作目錄中移除，如此它之後也不會身為未追蹤檔案而被你看到。
```go
$git rm Css.md
// git 對此檔案永遠排除
$git reset Css.md
// 將Css.md從預存區中剃除
```
2.如果已提交又想做更改
> 提交後，再git add，則輸入git commit --amend便可取代上一次提交
```go
$git commit --amend
```
***
## **遠端管理**
### **1.顯示設定好的遠端版本庫**
> 顯示 Git 用來讀寫的遠端簡稱及簡稱時所用的網址。
```go
$git remote -v
```
### **2.新增遠端版本庫**
```go
$git remote add [版本庫名稱] [url]
```
### **3.檢視遠端版本庫特定資訊**
> HEAD branch: master  如果你執行 git pull，它會在獲取所有遠端參照之後，自動將遠端的 master 合併到你的 master 分支。
```go
$git remote show [remote-name]

* remote origin
  Fetch URL: git@github.com:cosmic1330/Markdown_Note.gㄅ
  Push  URL: git@github.com:cosmic1330/Markdown_Note.git
  HEAD branch: master
  Remote branches:
    dev    tracked
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (local out of date)
```
### **4.重新命名遠端版本庫**
```go
$git remote rename [原名稱] [欲修改名稱]
```
### **5.下載遠端版本庫到本端**
> 下載後並不會自動合併你的任何工作內容，也不會自動修改你正在修改的東西； 當你準備好合併你的工作內容時，你必需用手動的方式進行合併。
```go
$ git fetch [remote-name] [refspec]

```
### **6.合併遠端數據庫的分支的修改內容**
> 可以把遠端數據庫修改的內容合併到本地端數據庫(pull = fetch + merge)
```go
$ git pull <repository> <refspec>
```
### **7.查看commit的訊息**
```go
$ git log --oneline --graph
//--graph 圖示表示
```
***
## **Git的進階應用 `分支`**
現在讓我們來看一個簡單的分支與合併的例子，實際工作中大體也會用到這樣的工作流程：

1. 開發某個網站。
2. 為實現某個新的需求，建立一個分支。
3. 在這個分支上開展工作。

假設此時，你突然接到一個電話說有個很嚴重的問題需要緊急修補，那麼可以按照下面的方式處理：

1. 返回到原先已經發佈到生產伺服器上的分支。
2. 為這次緊急修補建立一個新分支，並在其中修復問題。
3. 通過測試後，回到生產伺服器所在的分支，將修補分支合併進來，然後再推送到生產伺服器上。
4. 切換到之前實現新需求的分支，繼續工作。
### **何謂分支**
> 在數據庫進行最初的提交後，Git會建立一個名為master的分支。分支可自行增加
### **查看分支**
```go
$ git branch
//查看本地端分支
$ git branch -r
//查看遠端分支
$ git branch -a
//查看本地及遠端分支
```
### **創建新分支**
```go
$ git branch [新建分支名稱]
```
### **修改分支名稱**
```go
$ git branch -m <oldbranch> <newbranch>
```
### **刪除分支**
```go
$ git branch -d <branch>
```
### **切換到該分支**
```go
$git checkout [分支名稱]
//切換到現有分支
$git checkout -b [新建分支名稱]
//要新建並切換到該分支
```
> 當切換到iss53分支後修改檔案結束，切換回master進行分支合併
![修改後的分支與時程圖](/image/cheout.png)
```go
$ git merge [修改後的分支]
//修改後的分支內容將會合併於master
$git checkout -b [刪除修改後分支]
//合併後，修改的分支記得刪除
```
![修改後的分支與時程圖](/image/cheout2.png)
### **解決分支衝突**
> 
```go
$git mergetool
```
