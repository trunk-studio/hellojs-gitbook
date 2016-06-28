# Git Flow

![](./gitflow.png)


## 主要 branch

* master: 主要版本，只接受 develop 和 Release 的 merge
* develop: 所有 Feature 開發都從這分支出去，完成後 merge 回來

## 支援 branch

* feature branches：從 develop 分支出來，當功能開發修改完成後 merge 回 develop
* release branches：從 develop 分支出來，是準備釋出的版本，只修改版本號與 bug，完成後 merge 回 develop 與 master，並在 master 標上版本號的 tag
* hotfix branches：從 master 分支出來，主要是處理已釋出版本需要立即修改的錯誤，完成後 merge 回 develop 與 master，並在 master 標上版本號的 tag
