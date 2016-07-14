# 開始使用 git

## 專案初始

建立本地端數據庫：為了方便用戶個人使用，在自己的機器上配置的數據庫。

透過下列指令進行初始

`git init`

## 工作流程

### Working dir 新增檔案

工作目錄（Working Tree）是保存您目前正在處理檔案的目錄，Git 相關的操作都會在這個目錄下完成。


```
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
                 [--edit | -e] [--[no-]all | --[no-]ignore-removal | [--update | -u]]
                 [--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing]
                 [--] [<pathspec>...]
```

### 新增特定檔案

`git add <filename>`

### 新增全部檔案

`git add .`

### Index (stage)

索引(Index )位於工作目錄和數據庫之間，是為了向數據庫提交作準備的暫存區域。

```
git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>] [--amend]
          [--dry-run] [(-c | -C | --fixup | --squash) <commit>]
          [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
          [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
          [--date=<date>] [--cleanup=<mode>] [--[no-]status]
          [-i | -o] [-S[<keyid>]] [--] [<file>...]
```

`git commit -m "Commit message"`

工作目錄上做的任何變更並不會直接提交到數據庫的。Git在執行提交的時候，不是直接將工作目錄的狀態儲存到數據庫，而是將索引的狀態儲存到數據庫。因此，要提交變更，首先必需要把變更內容加入到索引中。

索引的存在可以排除工作目錄裡不必要的檔案提交，還可以只將檔案變更內容的一部分加入索引並提交。

### Repository

為集中管理的數據庫，每個人在 local 端所做的改變及 commit 都可以透過下列指令來更新數據庫

```
git push [--all | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
                  [--repo=<repository>] [-f | --force] [--prune] [-v | --verbose]
                  [-u | --set-upstream]
                  [--[no-]signed|--sign=(true|false|if-asked)]
                  [--force-with-lease[=<refname>[:<expect>]]]
                  [--no-verify] [<repository> [<refspec>...]]
```

### 練習創建第一個 git 版本控制專案

1. 新增資料夾 git-tutorial
2. 進入 git-tutorial 資料夾
2. 新增檔案 README.md
3. 執行 `git init` 初始化專案
4. 執行 `git add .` 加入所有變更的檔案
5. 執行 git commit -m 'init'
6. 完成第一個版本控制
