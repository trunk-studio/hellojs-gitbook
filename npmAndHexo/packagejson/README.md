## 目錄
- 概述
- scripts字段
- dependencies字段，devDependencies字段
- peerDependencies
- bin字段
- main字段
- config字段
- 其他
- browser字段
 - engines字段
 - man字段
 - preferGlobal字段
 - style字段


## 概述
每個項目的根目錄下面，一般都有一個package.json文件，定義了這個項目所需要的各種模塊，以及項目的配置信息（比如名稱、版本、許可證等元數據）。 npm install命令根據這個配置文件，自動下載所需的模塊，也就是配置項目所需的運行和開發環境。

下面是一個最簡單的package.json文件，只定義兩項元數據：項目名稱和項目版本。
```
{
  "name" : "xxx",
  "version" : "0.0.0",
}
```
上面代碼說明，package.json文件內部就是一個JSON對象，該對象的每一個成員就是當前項目的一項設置。比如name就是項目名稱，version是版本（遵守“大版本.次要版本.小版本”的格式）。

下面是一個更完整的package.json文件。
```
{
  "name": "Hello World",
  "version": "0.0.1",
  "author": "張三",
  "description": "第一個node.js程序",
  "keywords": [
    "node.js",
    "javascript"
  ],
  "repository": {
    "type": "git",
    "url": "https://path/to/url"
  },
  "license": "MIT",
  "engines": {
    "node": "0.10.x"
  },
  "bugs": {
    "url": "http://path/to/bug",
    "email": "bug@example.com"
  },
  "contributors": [
    {
      "name": "李四",
      "email": "lisi@example.com"
    }
  ],
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "latest",
    "mongoose": "~3.8.3",
    "handlebars-runtime": "~1.0.12",
    "express3-handlebars": "~0.5.0",
    "MD5": "~1.2.0"
  },
  "devDependencies": {
    "bower": "~1.2.8",
    "grunt": "~0.4.1",
    "grunt-contrib-concat": "~0.3.0",
    "grunt-contrib-jshint": "~0.7.2",
    "grunt-contrib-uglify": "~0.2.7",
    "grunt-contrib-clean": "~0.5.0",
    "browserify": "2.36.1",
    "grunt-browserify": "~1.3.0",
  }
}
```
下面詳細解釋package.json文件的各個字段。

## scripts字段
scripts指定了運行腳本命令的npm命令行縮寫，比如start指定了運行npm run start時，所要執行的命令。

下面的設置指定了npm run preinstall、npm run postinstall、npm run start、npm run test時，所要執行的命令。
```
"scripts": {
    "preinstall": "echo here it comes!",
    "postinstall": "echo there it goes!",
    "start": "node index.js",
    "test": "tap test/*.js"
}
```
## dependencies字段，devDependencies字段
dependencies字段指定了項目運行所依賴的模塊，devDependencies指定項目開發所需要的模塊。

它們都指向一個對象。該對象的各個成員，分別由模塊名和對應的版本要求組成，表示依賴的模塊及其版本範圍。
```
{
  "devDependencies": {
    "browserify": "~13.0.0",
    "karma-browserify": "~5.0.1"
  }
}
```
對應的版本可以加上各種限定，主要有以下幾種：

- 指定版本
 - 比如1.2.2，遵循“大版本.次要版本.小版本”的格式規定，安裝時只安裝指定版本。

- 波浪號（~）+ 指定版本
 - 比如~1.2.2，表示安裝1.2.x的最新版本（不低於1.2.2），但是不安裝1.3.x，也就是說安裝時不改變大版本號和次要版本號。

- 插入號（^）+ 指定版本
 - 比如ˆ1.2.2，表示安裝1.x.x的最新版本（不低於1.2.2），但是不安裝2.x.x，也就是說安裝時不改變大版本號。需要注意的是，如果大版本號為0，則插入號的行為與波浪號相同，這是因為此時處於開發階段，即使是次要版本號變動，也可能帶來程序的不兼容。

- latest：安裝最新版本。

package.json文件可以手工編寫，也可以使用npm init命令自動生成。

```
$ npm init
```
這個命令採用互動方式，要求用戶回答一些問題，然後在當前目錄生成一個基本的package.json文件。所有問題之中，只有項目名稱（name）和項目版本（version）是必填的，其他都是選填的。

有了package.json文件，直接使用npm install命令，就會在當前目錄中安裝所需要的模塊。
```
$ npm install
```
如果一個模塊不在package.json文件之中，可以單獨安裝這個模塊，並使用相應的參數，將其寫入package.json文件之中。
```
$ npm install express --save
$ npm install express --save-dev
```
上面代碼表示單獨安裝express模塊，--save參數表示將該模塊寫入dependencies屬性，--save-dev表示將該模塊寫入devDependencies屬性。

## peerDependencies
有時，你的項目和所依賴的模塊，都會同時依賴另一個模塊，但是所依賴的版本不一樣。比如，你的項目依賴A模塊和B模塊的1.0版，而A模塊本身又依賴B模塊的2.0版。

大多數情況下，這不構成問題，B模塊的兩個版本可以並存，同時運行。但是，有一種情況，會出現問題，就是這種依賴​​關係將暴露給用戶。

最典型的場景就是插件，比如A模塊是B模塊的插件。用戶安裝的B模塊是1.0版本，但是A插件只能和2.0版本的B模塊一起使用。這時，用戶要是將1.0版本的B的實例傳給A，就會出現問題。因此，需要一種機制，在模板安裝的時候提醒用戶，如果A和B一起安裝，那麼B必須是2.0模塊。

### peerDependencies字段
就是用來供插件指定其所需要的主工具的版本。
```
{
  "name": "chai-as-promised",
  "peerDependencies": {
    "chai": "1.x"
  }
}
```
上面代碼指定，安裝chai-as-promised模塊時，主程序chai必須一起安裝，而且chai的版本必須是1.x。如果你的項目指定的依賴是chai的2.0版本，就會報錯。

注意，從npm 3.0版開始，peerDependencies不再會默認安裝了。

## bin字段
bin項用來指定各個內部命令對應的可執行文件的位置。
```
"bin": {
  "someTool": "./bin/someTool.js"
}
```
上面代碼指定，someTool 命令對應的可執行文件為 bin 子目錄下的 someTool.js。 Npm會尋找這個文件，在node_modules/.bin/目錄下建立符號鏈接。在上面的例子中，someTool.js會建立符號鏈接npm_modules/.bin/someTool。由於node_modules/.bin/目錄會在運行時加入系統的PATH變量，因此在運行npm時，就可以不帶路徑，直接通過命令來調用這些腳本。

因此，像下面這樣的寫法可以採用簡寫。

```
scripts: {
  start: './node_modules/someTool/someTool.js build'
}

// 簡寫為
scripts: {
  start: 'someTool build'
}
```
所有node_modules/.bin/目錄下的命令，都可以用npm run [命令]的格式運行。在命令行下，鍵入npm run，然後按tab鍵，就會顯示所有可以使用的命令。

## main字段
main字段指定了加載該模塊時的入門文件，默認是模塊根目錄下面的index.js。

## config字段
config字段用於向環境變量輸出值。

下面是一個package.json文件。
```
{
  "name" : "foo",
  "config" : { "port" : "8080" },
  "scripts" : { "start" : "node server.js" }
}
```
然後，在server.js腳本就可以引用config字段的值。

http.createServer(...).listen(process.env.npm_package_config_port)
用戶可以改變這個值。
```
$ npm config set foo:port 80
```
## 其他
browser字段
browser指定該模板供瀏覽器使用的版本。 Browserify這樣的瀏覽器打包工具，通過它就知道該打包那個文件。
```
"browser": {
  "tipso": "./node_modules/tipso/src/tipso.js"
},
```
## engines字段
engines指明了該項目所需要的node.js版本。

## man字段
man用來指定當前模塊的man文檔的位置。
```
"man" :[ "./doc/calc.1" ]
```
## preferGlobal字段
preferGlobal的值是布爾值，表示當用戶不將該模塊安裝為全局模塊時（即不用–global參數），要不要顯示警告，表示該模塊的本意就是安裝為全局模塊。

## style字段
style指定供瀏覽器使用時，樣式文件所在的位置。樣式文件打包工具parcelify，通過它知道樣式文件的打包位置。
```
"style": [
  "./node_modules/tipso/src/tipso.css"
]
``
