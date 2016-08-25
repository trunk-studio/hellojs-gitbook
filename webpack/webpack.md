## webpack

#### 打包 ( Bundle ) 這件事

##### 對前端程式碼或是圖片、字型等 Assets 檔案進行一些轉譯、打包、壓縮、額外加工處理

### Wepack 是一個前端模組的整合與打包工具

- 同時支援 AMD、CommonJS、ES6 Module 等模組規範
- 能讓一些原本只能在 Node 上使用的 package 在前端中也能使用
- 高效能的 Bundle 速度
- 整合樣式表（CSS/SCSS/LESS 等）
- 能夠處理圖片以及字型檔
- 豐富的額外插件

#### webpack.config.js

##### Wepack 的設定檔，我們將運行的配置寫在這段程式碼中，然後 webpack 執行時就會按照該配置來進行 bundle的動作並產出靜態檔案。

```
var path = require('path');
var webpack = require('webpack');

module.exports = {

  entry: [
    // necessary for hot reloading with IE:
    'eventsource-polyfill',
    // listen to code updates emitted by hot middleware:
    'webpack-hot-middleware/client',
    // your code's enrty:
    './assets/main.jsx'
  ],

  output: {
    path: path.join(__dirname, 'dist'),
    filename: 'bundle.js',
    publicPath: '/dist/'
  },

  resolve: {
    root: [
      path.join(__dirname, 'assets')
    ],
    extensions: ['', '.js', '.jsx','css', '.scss']
  },

  module: {
    loaders: [{
      test: /\.(js|jsx)$/,
      loader: 'babel-loader',
      exclude: /node_modules/
    }, {
      test: /\.css$/,
      loader: 'style-loader!css-loader?sourceMap'
    }, {
      test: /\.scss$/,
      loader: 'style-loader!css-loader?sourceMap!sass-loader?sourceMap'
    }, {
      test: /\.(jpe?g|JPE?G|png|PNG|gif|GIF|svg|SVG|woff|woff2|eot|ttf)(\?v=\d+\.\d+\.\d+)?$/,
      loader: 'url?limit=1024&name=[sha512:hash:base64:7].[ext]'
    }]
  },

  devtool: 'cheap-module-eval-source-map',

  plugins: [
    new webpack.HotModuleReplacementPlugin(),
    new webpack.ProvidePlugin({
      React: 'react',
      ReactDOM:'react-dom',
      $: 'jquery'
    })
  ]
};
```

### entry

- 會被 bundle 出來的靜態檔案個體，以及其來源
- 如果是 Single Page Application 的話，可以考慮整個專案只有一個 entry
- 如果不是 SPA 的話，可以根據情況切出各頁面間自己專屬的 entry 以及共用的 entry

#### entry

```
entry: [
    // necessary for hot reloading with IE:
    'eventsource-polyfill',
    // listen to code updates emitted by hot middleware:
    'webpack-hot-middleware/client',
    // your code's enrty:
    './assets/main.jsx'
  ],
```

#### entry - Style

##### CSS 必須被 require 才會套用或產生

```
require('./index.scss');
```

##### 預設情況下（style-loader），被 require 的 CSS/SCSS 會被 JavaScript 動態的製造一個虛擬資源然後將 Bundle 好的 CSS 程式碼注入其中，而不會產生實體的 CSS 靜態檔案，因此也不需要在 HTML 中另外引入 CSS 檔案

```
<!DOCTYPE html>
<html>
 #shadow-root (open)
 <head>
 <meta charset="utf-8">
 <title>modern front-end workflow</title>
 <Link rel="stylesheet" href="blob:http://localhost:3000/ca131cb5-d803-4089-aab1-921212dd4621>
 </head>
</html>
```

### output

- path：Bundle 出的個體靜態檔案存放的位置
- publicPath：CSS 中引入 URL 時參考的路徑
- filename：Bundle 出的個體靜態檔案的名稱

##### output
```
output: {
    path: path.resolve(__dirname, 'build'), //webpack 建置專案的路徑
    publicPath: "http://localhost:3000/build/", //css引入url時參考的路徑
    filename: "[name].js"
  },
```


### resolve

- root => require 時路徑省略
- extensions => require 時副檔名省略

```
resolve: {
    root: [
      path.join(__dirname, 'assets')
    ],
    extensions: ['', '.webpack.js', '.web.js', '.js', '.jsx', '.scss', '.css', 'config.js']
  },
```

### module - loader

##### 資源處理加載器，Wepack 與其他 Assets 處理器溝通的橋樑

```
module: {
    loaders: [{
      test: /\.(js|jsx)$/,
      loader: 'babel-loader',
      exclude: /node_modules/
    }, {
      test: /\.css$/,
      loader: ExtractTextPlugin.extract('css-loader?sourceMap') //'style-loader!css-loader?sourceMap'
    }, {
      test: /\.scss$/,
      loader: ExtractTextPlugin.extract('css-loader?sourceMap!sass-loader?sourceMap') //'style-loader!css-loader?sourceMap!sass-loader?sourceMap'
    }, {
      test: /\.(jpe?g|JPE?G|png|PNG|gif|GIF|svg|SVG|woff|woff2|eot|ttf)(\?v=\d+\.\d+\.\d+)?$/,
      loader: 'url-loader?limit=1024&name=[sha512:hash:base64:7].[ext]'
    }]
  },
```

### watch

##### 監聽資源改變，自動重新 Bundle

```
watch: true
```

### devtool

##### 產生 JavaScript 檔案的 Source map，以便開發時 Debug

```
devtool: 'source-map'
```

### plugin - ExtractTextPlugin

##### 讓 Bundle 時產出實體的 CSS 靜態檔案

```
{
      test: /\.css$/,
      loader: ExtractTextPlugin.extract('css-loader?sourceMap') //'style-loader!css-loader?sourceMap'
    }, {
      test: /\.scss$/,
      loader: ExtractTextPlugin.extract('css-loader?sourceMap!sass-loader?sourceMap') //'style-loader!css-loader?sourceMap!sass-loader?sourceMap'
    },
```

### plugin - BrowserSync

- 監聽資源的改變並在 Bundle 完成後自動重新刷新頁面
- 同步多個視窗或是多台裝置在該頁面的事件操作
- 監聽額外檔案的改變

```
new BrowserSyncPlugin({
  host: 'localhost',
  port: 3000,
  proxy: 'localhost:8000',
  files: ['*.html']
})
```

### plugin - ProvidePlugin

##### 發現有指定的變數名稱時，自動 require 指定的模組

```
new webpack.ProvidePlugin({
  $: 'jquery',
  jQuery: 'jquery',
  'windows.jQuery': 'jquery',
  'root.jQuery': 'jquery',
})
```

### plugin - WebpackNotifierPlugin

##### 會在 Webpack bundle 發生錯誤時，跳出系統提示

```
new WebpackNotifierPlugin
```

### plugin - UglifyJsPlugin

- 壓縮、混淆 JavaScript 程式碼
- 因運算複雜，Bundle 速度非常緩慢
- 應當在正式的 Production 環境中才使用

```
new webpack.optimize.UglifyJsPlugin({
  sourceMap: false,
  mangle: false
})
```
