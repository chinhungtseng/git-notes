# git-notes

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

## 檢視紀錄
```
$ git log
```
* 其他參數
  * `-p` 
  * `--stat`
  * `--shortstat`
  * `--name-only`
  * `--name-status`
  * `abbrev-commit`
  * `--relative-date`
  * `--graph`
  * `--pretty` 
  * `--oneline` same as `--pretty=oneline --abbrev-commit`

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

## 修改 commit 紀錄
* 修改最近一次 commit 訊息
```
$ git commit --amend -m "<commit-message>"
```
* 修改歷史 commit 訊息
```
git rebase -i <commit-to>
```











