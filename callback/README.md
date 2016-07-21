# Callback

## Example
```javascript
function Add( num, callback ) {
    num = num + 1;
    callback( num );
}

Add( 2, function( ans ) {
    console.log( ans ); // 3
});
```

## Why we need it?
  * 為了防止資料還沒收到就結束程式或回傳參數
  * 最常使用的地方
    * ajax
    * call api
    * search DB

## [JSON](https://zh.wikipedia.org/wiki/JSON) type
```JSON
// get article list
[
  {
    "id": 1,
    "title": "post 1"
  },
  {
    "id": 2,
    "title": "post 2"
  },
  {
    "id": 3,
    "title": "post 3"
  }
]
```

```JSON
// get article information

{
    "id": 1,
    "authorId": 2,
    "content": "今天天氣真好"
}
```

```JSON
// get author information
{
    "id": 2,
    "name": "Deleav",
    "email": "deleav@gmail.com"
}
```

## [AJAX](https://zh.wikipedia.org/wiki/AJAX) function
```javascript
// get article list
function getArticleList( callback ) {
    $.ajax({
        url: "/api/article",
        type: "get"
    }).done(function( articleList ) {
        callback( articleList );
    });
}
```

```javascript
// get article
function getArticle( id, callback ) {
    $.ajax({
        url: "/api/article" + id,
        type: "get"
    }).done(function( article ) {
        callback( article );
    });
}
```

```javascript
// get author name
function getAuthor( authorId, callback ) {
    $.ajax({
        url: "/api/author",
        type: "post",
        body: {
            id: authorId
        }
    }).done(function( authorInfo ){
        callback( authorInfo );
    });
}
```

## 取得文章列表
```javascript
// get article list
function getArticleList( callback ) {
    $.ajax({
        url: "/api/article",
        type: "get"
    }).done(function( articleList ) {
        callback( articleList );
    });
}

getArticleList(function( articleList ) {
    console.log( articleList );
});
```
```JSON
// get article list
[
  {
    "id": 1,
    "title": "post 1"
  },
  {
    "id": 2,
    "title": "post 2"
  },
  {
    "id": 3,
    "title": "post 3"
  }
]
```

## 取得第一篇文章的內容
```javascript
// get article list
function getArticleList( callback ) {
    $.ajax({
        url: "/api/article",
        type: "get"
    }).done(function( articleList ) {
        callback( articleList );
    });
}
// get article
function getArticle( id, callback ) {
    $.ajax({
        url: "/api/article/" + id,
        type: "get"
    }).done(function( article ) {
        callback( article );
    });
}
```

```javascript
getArticleList(function( articleList ) {
    getArticle(articleList[0].id, function( articleInfo ) {
        console.log( articleInfo );
    });
});
```

```JSON
// get article information
{
    "id": 1,
    "authorId": 2,
    "content": "今天天氣真好"
}
```

## 取得第一篇文章的作者資訊
```javascript
getArticleList(function( articleList ) {
    getArticle(articleList[0].id, function( articleInfo ) {
        getAuthor(articleInfo.arthorId, function( arthorInfo ) {
            console.log( arthorInfo );
        });
    });
});
```

```JSON
// get author information
{
    "id": 2,
    "name": "Deleav",
    "email": "deleav@gmail.com"
}
```

# Promise
  * 在 return 值外面包一層 Promise
  * Promise 是個物件，有許多的 method 能夠使用（ ex: then, catch...等 ）
```javascript
// get article list
function getArticleList( callback ) {
    return new Promise(function( resolve, reject ) {
        $.ajax({
            url: "/article",
            type: "get"
        }).done(function( articleList ) {
            return resolve( articleList );
        });
    }
}

// get article
function getArticle( id, callback ) {
    return new Promise(function( resolve, reject ) {
        $.ajax({
            url: "/article/" + id,
            type: "get"
        }).done(function( article ) {
            return resolve( article );
        });
    }
}

// get author name
function getAuthor( authorId, callback ) {
    return new Promise(function( resolve, reject ) {
        $.ajax({
            url: "/author",
            type: "post",
            body: {
                id: authorId
            }
        }).done(function( authorInfo ){
            return resolve( authorInfo );
        });
    }
}
```

```javascript
// 原本
getArticleList(function( articleList ) {
    getArticle(articleList[0].id, function( articleInfo ) {
        getAuthor(articleInfo.arthorId, function( arthorInfo ) {
            console.log( arthorInfo );
        });
    });
});

// Promise ( ES6 )
getArticleList().then(function( articleList ) {
    return getArticle( articleList[0].id );
}).then(function( article ) {
    return getArticle( article.authorId );
}).then(function( authorInfo ) {
    console.log( authorInfo );
});

// result
{
    "id": 2,
    "name": "Deleav",
    "email": "deleav@gmail.com"
}
```

# Arrow function
  * =>
  * http://babeljs.io/repl/
```javascript
// Promise ( ES6 )
getArticleList().then(function( articleList ) {
    return getArticle( articleList[0].id );
}).then(function( article ) {
    return getArticle( article.authorId );
}).then(function( authorInfo ) {
    console.log( authorInfo );
});

// Promise + arrow function ( ES6 )
getArticleList()
.then( articleList => getArticle( articleList[0].id ))
.then( article => getArticle( article.authorId ))
.then( authorInfo => {
    console.log( authorInfo )
});
```

# Async and await
  * 一定要用 Promise 包起來才能夠使用
  * 想要用 `await` 一定要加 `async`
```javascript
async function() {
    var articleList = await getArticleList();
    var article = await getArticle(articleList[0].id);
    var authorInfo = await getAuthor(article.authorId);
    console.log( arthorInfo );
}
```

```javascript
async () => {
    var articleList = await getArticleList();
    var article = await getArticle(articleList[0].id);
    var authorInfo = await getAuthor(article.authorId);
    console.log( arthorInfo );
}
```
