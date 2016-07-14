# update & merge

`git pull`

`git merge <branch>`

### merge 之前確認差異

`git diff <branch>`


## 練習

### 創建 git 版本控制專案

1. 新增資料夾 git-tutorial
2. 進入 git-tutorial 資料夾
2. 新增檔案 README.md
3. 執行 `git init` 初始化專案
4. 執行 `git add .` 加入所有變更的檔案
5. 執行 git commit -m 'init'


### 建立 develop 分支

1. 執行 `git branch develop`
2. 切換到 develop 分支 `git checkout develop`
3. 修改 README.md 新增 `hello develop branch`
4. 執行 git commit -m 'add develop branch'
5. 執行 `git log --graph --oneline --decorate --all`
6. 確認已有新的分支產生

### checkout master 並且 merge develop

1. 透過 `git checkout master` 回到 master 分支
2. 執行 `git merge develop` 完成 merge
3. 執行 `git commit -m 'merge develop'` 將變更提交
4. 執行 `git log --graph --oneline --decorate --all`
5. 確認 develop 分支已 merge 回 master
