# pull

欲同步遠端數據庫以更新本地端數據庫，請使用Pull(拉取)。

執行pull之後，會從遠端數據庫下載最新的修改歷史，將其同步到自己的本地端數據庫。

## 執行指令 pull

`git pull`

## fast-forward 合併

將遠端分支合併到我們的本地端分支


## 練習

### clone git-hello-world

1. 進入網址 <https://github.com/agileworks-tw/git-hello-world>
2. 取得 https git url
3. 執行 `git clone <https git url>`
4. 確認專案以複製完成

### pull 最新的修正

1. 由講師修改 README.md 新增 `hello guys`
2. `git add README.md`
3. `git commit -m 'new push'`
4. 由講師 push 最新的更動
2. 學員進入 git-hello-world 資料夾
3. 執行 `git pull`
4. 執行 `git log --graph --oneline --decorate --all`
5. 確認最新的 index 及檔案更動已更新
