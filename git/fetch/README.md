# Fetch

執行 pull，遠端數據庫的內容會自動合併。但是，有時候只是想確認遠端數據庫的內容卻不是真的想合併，在這種情況下，請使用 fetch。

執行 fetch，可以取得遠端數據庫的最新歷史記錄。取得的提交會導入在自動建立的分支中，並可以切換這個名為 FETCH_HEAD 的分支。


## 練習

### clone git-hello-world

1. 進入網址 <https://github.com/agileworks-tw/git-hello-world>
2. 取得 https git url
3. 執行 `git clone <https git url>`
4. 確認專案以複製完成

### pull 最新的修正

1. 由講師修改 README.md 新增 `hello guys for fetch`
2. `git add README.md`
3. `git commit -m 'new push for fetch'`
4. 由講師 push 最新的更動
2. 學員進入 git-hello-world 資料夾
3. 執行 `git fetch origin`
4. 執行 `git log --graph --oneline --decorate --all`
5. 確認最新的 index 已更動，但檔案還在目前的狀態。
6. 透過 `git merge origin/master` 將目前專案更新到最新的狀態
7. 再次透過 `git log --graph --oneline --decorate --all` 確認狀態
