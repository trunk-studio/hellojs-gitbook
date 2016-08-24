## hashHistory

### hashHistory 使用 URL Hash 來做 Front-End Routing

- ex: localhost/#/news/

- 優點：因為這個技術是很早以前就有的所以可以支援到很舊的瀏覽器

- 缺點：產生出來的網址後面會有亂數（不美觀）

## browserHistory

### browserHistory 使用瀏覽器的 History API 來做 Front-End Routing

- ex:localhost/news/

- 需要後端 Routing 設定的配合，否則重新整理會 404

- 當你要讓所有 Server-Side Route 都指向包含 React Application 的 View

- 必須將以下這段程式碼放在最後面
```
'*':{
  view:{ index }
}
```

- Route參數可以在component裡面取得

- 如下面這段程式碼
```
<Route path='/about/:name' component={AboutPage}/>
this.props.params.name
```

- ( ) 表示 URL 的這部分是非必要的

- 如下面這段程式碼
```
<Route path='/about(/:name)' />
// 匹配/about
// 匹配/about/name
```

- `*`則表示萬用字元

```
<Route path='/files/*' />
// 匹配/files
// 匹配/files/a
// 匹配/files/a/b
```

### Link

- 在 React 中使用 <a> 沒有意義，會導致整個頁面重載而非 Front-End Routing
- <Link> 是 <a> 的 React Front-End Routing 版本
-  使用 to 來代替 href

ex:
```
<Link to="/counter">counter</Link>
```

### browserHistory.push

- browserHistory.push 方法用於想透過程式呼叫來跳轉 Route 時

```
var inputSearchString = "test";
browserHistory.push(`/news/search/${ inputSearchString}`);
```
