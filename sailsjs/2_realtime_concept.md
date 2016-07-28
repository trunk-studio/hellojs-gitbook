# Socket.io
  * http://socket.io/

```bash
mkdir chat
cd chat
npm init --yes
npm install --save express@4.10.2
npm install --save socket.io

touch index.js
edit index.js
```

```javascript
var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  console.log('a user connected');

  socket.broadcast.emit('hi');

  socket.on('disconnect', function(){
    console.log('user disconnected');
  });

  socket.on('chat message', function(msg){
    io.emit('chat message', msg);
  });
});

http.listen(process.env.PORT || 3000, function(){
  console.log('listening on *:3000');
});
```

```bash
touch index.html
edit index.html
```

```html
<!doctype html>
<html>
  <head>
    <title>Socket.IO chat</title>
    <style>
      * { margin: 0; padding: 0; box-sizing: border-box; }
      body { font: 13px Helvetica, Arial; }
      form { background: #000; padding: 3px; position: fixed; bottom: 0; width: 100%; }
      form input { border: 0; padding: 10px; width: 90%; margin-right: .5%; }
      form button { width: 9%; background: rgb(130, 224, 255); border: none; padding: 10px; }
      #messages { list-style-type: none; margin: 0; padding: 0; }
      #messages li { padding: 5px 10px; }
      #messages li:nth-child(odd) { background: #eee; }
    </style>
  </head>
  <body>
    <ul id="messages"></ul>
    <form action="">
      <input id="m" autocomplete="off" /><button>Send</button>
    </form>

    <script src="http://code.jquery.com/jquery-1.11.1.js"></script>
    <script src="/socket.io/socket.io.js"></script>
    <script>
          var socket = io();

          $('form').submit(function(){
            socket.emit('chat message', $('#m').val());
            $('#m').val('');
            return false;
          });

          socket.on('chat message', function(msg){
             $('#messages').append($('<li>').text(msg));
          });
    </script>

  </body>
</html>
```

  * Publish to heroku
  * create a project on heroku.com
  * create a project on github.com

```bash
git init
git add .
git commit -m 'update files'
git push origin master
```
