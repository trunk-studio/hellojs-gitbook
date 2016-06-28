# 標籤

Git中，標籤有兩種類型：輕量標籤(lightweight tag)和標示標籤(annotated tag)。

常用於 master 之 production release(正式發佈) 版號。

## 輕量標籤

* 不可變更的暫時標籤
* 可以添加名稱

## 標示標籤

* 可以添加打標簽者的名稱、email及日期
* 可以添加名稱
* 可以添加註解
* 可以添加簽名

## tagging

`git tag <tagname>`
`git tag 1.0.0`

## 列出所有 tag

`git tag`

## 查詢詳細 tag 資訊

`git log --decorate`

## 開啟編輯器邊寫註解

`git tag -a <tagname>``

## 直接編寫註解

`git tag -am "連猴子都能懂的Git" 1.0.0`

## 刪除 tag

`git tag -d <tagname>`


標籤可以與 checkout 及 reset 命令搭配使用，可以簡單的使用標籤指向特定的提交。
