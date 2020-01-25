# git-notes

## 參考書籍
* [為自己學 git](https://gitbook.tw)
* [pro git 2](https://github.com/progit/progit2)

## 什麼是 git
* `git` 是開源的分散式版本控制系統
* `github` 為共同協作的一個平台(商業網站)，本體為 `git server`

## 安裝 git
* macOS
```
$ brew install git
```
* linux 
```
$ sudo yum install git
```

## git 設定檔
* 全域設定，使用 `--global`
```
$ git config --global user.name <user-name>
$ git config --global user.email <user-email>
```

* 針對特定資料夾(專案)設定，使用 `--local`
```
$ git config --local user.name <user-name>
$ git config --local user.email <user-email>
```

* 查看設定檔
```
$ git config --list
```
```
$ cat .git/config
```

* 設定 git cli 別名
```
$ git config --global alias.s status
$ git config --global alias.c commit
$ git config --global alias.l "log --oneline --graph --all"
```

## 新增 git repositories
* 現有專案初始化
```
$ git init
```
* clone 遠端專案
```
$ git clone <url>
$ git clone https://github.com/tidyverse/dplyr.git
```
* 取消 git 
```
$ rm -r .git
````

## Recording Changes to the Repository
* git 檔案分為四種狀態
  * Untracked
  * Unmodified
  * Modified 
  * Staged
  
* 查看 git repositories 狀態
```
$ git status
```
* 輸出簡短資訊，加上`-s`參數
```
$ git status -s
```

## 將檔案從工作目錄加入 git (staged)
* 單一檔案
```
$ git add <file>
```
* 所有檔案
```
$ git add --all
```
* 加入空資料夾
先在資料夾中新增任ㄧ空檔案，ex:> `.gitkeep`
```
$ touch <empty_dir>/.gitkeep
$ git add <empty_dir>/.gitkeep
```
* 只選擇部分區塊
```
$ git add -p <file>
```
## 將暫存區(staged)內容提交到 git 倉庫
```
$ git commit -m "<your-commit-message>"
```
* commit 空的內容
```
$ git commit --allow-empty -m "<commit-message>"
```
* add 結合 commit
```
$ git commit -a -m "<commit-message>"
```

## 刪除檔案
* 直接刪除
```
$ rm <file>
$ git add <deleted file> # 將刪除檔案加入暫存區
```
* 使用 git 刪除，會直接將刪除檔案加入暫存區
```
$ git rm <file> 
```
* 保留檔案，但將檔案從暫存區移除
```
$ git rm --cached <file>
```

## 變更檔名
```
$ git mv <file_from> <file_to>
```

## 檢視 commit 紀錄
```
$ git log
```
* 檢視特定檔案
```
$ git log <file>
```
* 檢視特定檔案每次 commit 做過的修改
```
$ git log -p <file>
$ git show <file/commit>
```
* 檢視每次 commit 新刪修的數量
```
$ git log --stat
```
* 以特定的格式呈現
```
$ git log --pretty=format
$ git log --color --graph --pretty=format:'%C(bold white)%h%Creset -%C(bold green)%d%Creset %s %C(bold green)(%cr)%Creset %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
```
* 以圖形方式呈現
```
$ git log --oneline --graph
$ git log --pretty=oneline --abbrev-commit --graph
```
* 尋找特定日期範圍
```
$ git log --since=<datetime> --until=<datetime> 
$ git log --after=<datetime> --before=<datetime>
```
* 尋找 commit 檔案內容中關鍵字
``` 
$ git log -S <word>
```
* 尋找 commit 訊息中關鍵字
```
$ git log --grep=<word>
```
* 尋找某人的commit
```
$ git log --auther=<name>
$ git log --committer=<name>
```
* reference logs
```
$ git log
```

## 修改 commit 紀錄
* 修改最近一次 commit 訊息
```
$ git commit --amend -m "<commit-message>"
```
* 修改歷史 commit 訊息
```
git rebase -i <commit-to>
```
* 追加檔案到最近一次 commit，不修改 commit 訊息
```
$ git commit -a --amend --no-edit
```
* 追加檔案到最近一次 commit，修改 commit 訊息
```
$ git commit -a --amend -m "<new-commit-message>"
```

## 忽略檔案規則
* 專案目錄中建立`.gitignore`檔案，將要忽略檔案名稱寫入`.gitignore`檔案中
```
$ touch .gitignore
```
* 無視`.gitignore`規則
```
$ git add -f <file>
```
* `.gitignore`的規則只對建立後的檔案有效，如要套用規則，需使用`git rm --cached`將檔案逐一移出追蹤，或使用`git clean -fx`全部清除在規則內被忽略的檔案

## 取消修改被修改檔案
將暫存區的檔案拉回(覆蓋)工作目錄的檔案
```
$ git checkout -- <file>
```
> git checkout <branch> 後面接分支為切換分支

## 重做 commit 
* 直接選取 commit
```
$ git reset <commit>
```
* 使用相對方式
回到距離 HEAD 前3個 commit 的位置
```
$ git reset HEAD~3 <commit>
$ git reset HEAD^^^ <commit>
```
> ^n 為第個順位的 parent commit 

* reset 主要有3種模式：`--mixed`、`--soft`和`--hard`，`--mixed`為預設模式

| 模式              | mixed mode   | soft mode  | hard mode |
| ----------------- | ------------ | ---------- | --------- |
| 工作目錄          | 不變         | 不變       | 丟掉      |
| 暫存區            | 丟掉         | 不變       | 丟掉      |
| commit 拆出來檔案 | 丟回工作目錄 | 丟回暫存區 | 直接丟掉  | 

* 另一種重做方式，較 `reset` 保險，因會新增一個 commit q代表回復的狀態
```
$ git revert <commit>
```

## 查看 git 物件
* 查看類型
```
$ git cat-file -t <object hash>
```
* 查看內容
```
$ git cat-file -p <object hash>
```

## 分支
* 查看分支狀態
```
$ git branch
```
* 建立分支
```
$ git branch <branch-name>
```
* 刪除分支
```
$ git branch -d <branch-name>
$ git branch -D <branch-name> #force delete
```
* 變更分支名稱
```
$ git branch -m <branch-name>
```
* 切換分支
```
$ git checkout <branch-name>
```
* 切換分支時如無分支就建立該分支
```
$ git checkout -b <branch-name>
```
* 合併分支
```
$ git merge <branch>
```



