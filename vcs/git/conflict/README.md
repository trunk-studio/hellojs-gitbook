# 編修衝突

如果遠端數據庫和本地端數據庫的同一個地方都發生了修改的情況下（例：檔案中同一行的地方）。
這時，因為Git不能自動判斷要導入那一個修改內容於是就會發生錯誤。

發生衝突的地方，Git會修改檔案的內容如下面程式碼。所以衝突的地方就需要手動修改。

```
<<<<<<< HEAD
test master

hello git
=======
test testbranch


hello
>>>>>>> testbranch
```

## 編修衝突練習


### master 新增 temp.md

1. 在 master 分支新增 temp.md
2. 將檔案透過 `git add temp.md` 加入 index
3. `git commit -m 'add temp.md'`

### hotfix 修改 temp.md

1. 在 master 的 `HEAD` 建立分支並切換透過指令 `git checkout -b hotfix`
2. 編輯 temp.md 在第一行寫入 `hello`
3. `git add temp.md` 加入 index
4. `git commit -m 'add hello in temp.md'`

### master 平行修改 temp.md

1. 切回 master 分支 `git checkout master`
2. 編輯 temp.md，此時此檔案無任何內容，第一行加入 `world`
4. `git commit -m 'add world in temp.md'`

### master merge hotfix 並且編修衝突

1. git merge hotfix
2. 將會出現如下的衝突

  ```
  <<<<<<< HEAD
  world
  =======
  hello
  >>>>>>> testbranch
  ```
3. 編修內容為 `hello world`
4. 編修完衝突之後把衝突的檔案透過 `git add temp.md` 再次加入 index
5. `git commit -m 'fix fonflict'` 完成衝突編修
