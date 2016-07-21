# Hexo

什麼是 Hexo ？

Hexo 是基於 Node.js 網誌框架，文章的寫作只要使用 Markdown 語法，Hexo 就能解析轉成靜態頁面

，且有許有多主題套件可以做更換。

## 安裝

安裝 Hexo 前，需先完成以下事項：

- Node.js 安裝
- Git 安裝
- 建立 [Git SSH Key](ssh_key.md)

上述事項完成後，使用 NPM 安裝 Hexo

```
$ npm install -g hexo-cli
```

Hexo 安裝完成後，使用 Hexo 生成 blog

```
$ hexo init folder-name

// 建置指定資料夾，和所需檔案

$ cd folder-name

// 進入指定資料夾

$ hexo s

$ hexo server

// 在本地端開啟預覽查看
```

## 環境設定

Hexo 的環境設定大多都由 `_config.yml` 這一個檔案做修改

不過需要注意的是在 Hexo 生成的資料夾中 `/themes/` 底下也有 `_config.yml`

一個是操作整個網誌的環境設定，另外一個則是操作主題的設定

在設定時需要注意

## deploy

再把本地中的 Hexo 檔案部署到 Github pages 上，須先在網誌的 `_config.yml` 上做設定，並安裝相關部署套件

- 安裝套件

```
$ npm install hexo-deployer-git --save
```

- `_config.yml` 設定

```
url:
 // 網站的網址
root:
 // 網站根目錄
permalink: :year:month:day/:title/
 // 文章的連結格式
```

`url` 、 `root` 未設定 deploy 上去的 blog 會發生以下圖例

![hexo-borken](/images/hexo-borken.png)

```
deploy:
  type: git
  // 要使用的部署類型
  repo: <repository url>
  // 要部署的專案位置
  branch: [branch]
  // 分支名稱
```

設定完成後，就可以下指令把網誌部署到 Github 上了！

```
$ hexo deploy

$ hexo d
```

指令說明

```
$ hexo clean
```

清除快取檔案或是以產生的靜態檔案

## theme



## 參考資料

[Hexo 官方文件](https://hexo.io/zh-tw/docs/)
