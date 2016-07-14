# checkout

checkout 可用於將特定版本檔案取出，無論是資料夾或檔案皆可

## 取出特定檔案

`git checkout <filename>`

## 取出特定資料夾

`git checkout <foldername>`

## 取出特定分支

`git checkout <branchname>`



## 練習


### 練習專案初始

1. 新增資料夾 git-tutorial
2. 進入 git-tutorial 資料夾
2. 新增檔案 README.md
3. 執行 `git init` 初始化專案
4. 執行 `git add .` 加入所有變更的檔案
5. 執行 git commit -m 'init'
6. 完成第一個版本控制

### 進行修改後透過 checkout 復原修改

1. 編輯 README.md 在第一行寫入 `hello world` 存檔離開
2. 透過 `git status` 確認目前修改狀態
3. 執行 `git checkout README.md` 將檔案復原
4. 執行 `git status` 確認目前已無最新的變動
