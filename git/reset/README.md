# reset

## 放棄所有 local file change

```
git fetch origin
git reset --hard origin/master
```

## 檔案 unstaged

也就是取消 `git add <file>` 把檔案加入 index，回覆到未加入前

`git reset <filename>`

## reset 的類型及主要使用的場合

* 復原修改過的索引的狀態(mixed)
* 徹底取消最近的提交(hard)
* 只取消提交(soft)


## 練習

### 創建 git 版本控制專案

1. 新增資料夾 git-tutorial
2. 進入 git-tutorial 資料夾
2. 新增檔案 README.md
3. 執行 `git init` 初始化專案
4. 執行 `git add .` 加入所有變更的檔案
5. 執行 git commit -m 'init'

### 執行檔案編修

1. 修改 README.md 新增 `hello reset`
2. 執行 `git add README.md` 將檔案加入 index
4. 執行 `git commit -m 'add test'`

### 執行 soft reset

5. 執行 `git log --graph --oneline --decorate --all` 確認目前狀態
1. 確認上一個 commit hash code，記住 hashcode 前 5 碼如： `7f3ab`
3. 執行 `git reset --soft 7f3ab`
5. 執行 `git log --graph --oneline --decorate --all`
6. 確認 commit 已復原
7. 再次進行 commit(不需再執行 git add) `git commit -m 'add test'`
8. 執行 `git log --graph --oneline --decorate --all`
9. 確認已再次 commit


### 執行 mixed reset

5. 執行 `git log --graph --oneline --decorate --all` 確認目前狀態
1. 確認上一個 commit hash code，記住 hashcode 前 5 碼如： `7f3ab`
3. 執行 `git reset --mixed 7f3ab`
5. 執行 `git log --graph --oneline --decorate --all`
6. 確認 commit 已復原
7. 執行 `git status` 確認有檔案變動，但尚未加入 index
2. 執行 `git add README.md` 將檔案加入 index
4. 執行 `git commit -m 'add test'`

## 執行 hard reset

5. 執行 `git log --graph --oneline --decorate --all` 確認目前狀態
1. 確認上一個 commit hash code，記住 hashcode 前 5 碼如： `7f3ab`
3. 執行 `git reset --hard 7f3ab`
5. 執行 `git log --graph --oneline --decorate --all`
6. 確認 commit 已復原
7. 執行 `git status` 確認無檔案變動，恢復為最原先的狀態
