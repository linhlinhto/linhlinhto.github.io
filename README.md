const express = require('express');
const fs = require('fs');
const http = require('http');
const WebSocket = require('ws');
const bodyParser = require('body-parser');

const app = express();
const server = http.createServer(app);
const wss = new WebSocket.Server({ server });

let latestFrame = null;

app.use('/upload', bodyParser.raw({ type: 'image/jpeg', limit: '5mb' }));

app.post('/upload', (req, res) => {
  latestFrame = req.body.toString('base64');
  wss.clients.forEach(client => {
    if (client.readyState === WebSocket.OPEN) {
      client.send(latestFrame);
    }
  });
  res.send("OK");
});

app.get('/', (req, res) => {
  res.send(`
    <!DOCTYPE html>
    <html>
    <head><title>ESP32-CAM Stream</title></head>
    <body>
      <h1>ESP32-CAM Live</h1>
      <img id="video" src="loading.jpg" />
      <script>
        const ws = new WebSocket('wss://' + location.host + '/ws');
        ws.onmessage = function(event) {
          document.getElementById('video').src = 'data:image/jpeg;base64,' + event.data;
        };
      </script>
    </body>
    </html>
  `);
});

wss.on('connection', socket => {
  if (latestFrame) {
    socket.send(latestFrame);
  }
});

server.listen(3000, () => {
  console.log("✅ Server running at http://localhost:3000");
});
