# Route
  * cd firstApp
  * touch views/todo.ejs  
  * sails generate api Task
  * firstApp/config/routes.js↓

```javascript
-------------------------routes.js-------------------------------------
  '/': {
    view: 'homepage'
  },

  '/todo' :{
      view:'todo'
  }
  -------------------------------------------------------------------------
```
  * 記得要存檔  (Crtl+S)

```html
 ---------------------"views/todo.ejs"--------------------------------
 <h1> todo list</h1>
<hr>

<ul></ul>

<hr>

<form action="/task/create" method="POST">
    <input type="text" name="title" placeholder="Please your task here..">
    <input type="submit" value="Submit">
</form>

 -----------------------------------------------------------------------------
```

  * npm start
    * 選擇 2 保留資料
    * 選擇 3 清除資料
  * 中斷執行 Crtl+C

```html
  ---------------------"views/todo.ejs"--------------------------------
<h1>Todo list</h1>
<hr>

<ul></ul>

<hr>
<form action="/task/create" method="POST">
    <input type="text" name="title" placeholder="請填入您的大名">
    <input type="submit" value="加入">
</form>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.3/jquery.js"> </script>

<script>
$.get(" /task", function (result) {
    var tempHtml= "";
    console.log(result);

    for(var i=0;i<result.length; i++){
        tempHtml = tempHtml + "<li>" +
        "<button class='delete' data-id='"
        + result[i].id +"'>移除</button> "
        + result[i].title + "</li>";
    }

    $("ul").html(tempHtml);

    $("button.delete").on("click", function(e) {
        $.get("/task/destroy/" + $(this).data("id") , function (){
            window.location.reload();

        });
    });    
});

$("form").on("submit", function (e) {

    $.post("/task/create", {
        title: $("input[name=title]").val()
    },function (result) {
        window.location.reload();
    })

    return false;
});


</script>

 -----------------------------------------------------------------------------
```

  * npm start
    * 選擇 2 保留資料
    * 選擇 3 清除資料

```javascript
-----------------------"views/todo.ejs"--------------------------------
底下新增

$("form").on("submit" , function (e) {
    $.post("/task/create",{
        title: $("input[name=title]").val()
        }, function (result){
            window.location.reload();
        })

        return false;
    });
```

  * 刪除按鍵
```javascript
   for(var i=0;i<result.length; i++){
        tempHtml = tempHtml + "<li>"+
        "<button class='delete'data-id='" +
        result[i].id  +
        "'>Delete   </button>  "
        + result[i].title + "</li>";
    }

    $("ul").html(tempHtml);

    $("button.delete").on("click",function (e) {

       $.get("/task/destroy/" + $(this).data("id") , function()

       {
        window.location.reload();
        });
     });
  });
-----------------------------------------------------------------------------
```

```javascript
----------------------------config/models.js--------------------------
  migrate: 'alter'  //保持

-----------------------------------------------------------------------------
```
