var app = require('express')();
var http = require('http').Server(app);
var io = require('socket.io')(http);
var sockets = {};
//var clients = io.sockets.clients()

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  console.log('a user connected');
  socket.id = Math.random();
  socket.on('send-username', function(username){
    socket.username = username
    //users.push(socket.nickname);
  });
  sockets[socket.id] = socket;
  socket.on('chat message', function(msg){
    console.log(socket.username + ": " + msg);
    //console.log(Object.keys(clients));
    io.emit('chat message', msg);
  });
  socket.on('disconnect', function(){
    console.log('user disconnected');
  });
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});
