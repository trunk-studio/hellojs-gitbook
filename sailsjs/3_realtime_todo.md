# Realtime todo
### Library and Framework
  * Games of JavaScript & HTML5
    * http://browserquest.mozilla.org/    
    * http://www.playkeepout.com/        
    * https://developer.cdn.mozilla.net/media/uploads/demos/a/z/azakai/3baf4ad7e600cbda06ec46efec5ec3b8/bananabread_1424465008_demo_package/index.html
    * http://media.tojicode.com/q3bsp/
  * Framework
    * http://pomelo.netease.com/
    * http://www.createjs.com/
  * Source code
    * https://github.com/mozilla/BrowserQuest

### introduce angular.js
  * https://angularjs.org/
  * https://ajax.googleapis.com/ajax/libs/angularjs/1.2.29/angular.min.js

```html
---------------------------layout-----------------
<body ng-app ng-controller="taskController">
---------------------------todo-------------------
<li ng-repeat="task in tasks">
  {{task.title}}
</li>
```
 
```html
<head>
  <!--SCRIPTS-->
  <script src="/js/dependencies/sails.io.js"></script>
  <!--SCRIPTS END-->
</head>
```
```javascript
function taskController($scope) {
  io.socket.on("connect", function () {
    io.socket.get("/task", function (tasks) {
      console.log(tasks);
      $scope.tasks = tasks;
      $scope.$apply();
    });
  });
}
```
```html
<h1>TaS list/h1>
<hr>

<ul>
    <li ng-repeat="task in tasks">
        {{task.title}}
    </li>
</ul>

<hr>
<form action="/task/create" method="POST">
    <input type="text" name="title" placeholder="請填入您的大名">
    <input type="submit" value="加入">
</form>

<script src="
https://ajax.googleapis.com/ajax/libs/angularjs/1.2.29/angular.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/1.11.3/jquery.js"> </script>

<script>
function taskController($scope) {
  io.socket.on("connect", function () {
    io.socket.get("/task", function (tasks) {
      $scope.tasks = tasks;
      $scope.$apply();
    });
  });
}


$("form").on("submit", function (e) {

    $.post("/task/create", {
        title: $("input[name=title]").val()
    },function (result) {
        window.location.reload();
    });

    return false;
});


</script>
```
```html
---------------------------todo-----------------
  <input type="text" ng-model="task" name="title" placeholder="請填入您的大名">
  <input type="submit" ng-click="submitHandler()" value="Submit">
```
```javascript
$scope.submitHandler = function() {
  io.socket.post("/task", {
    title: $scope.task
  }, function (result) {
    $scope.tasks.push(result);
    $scope.$apply();
  });
};
```
```bash
---------------------git hub------------------------
git add .
git commit -m 'update file'
git push origin master
```
