<!DOCTYPE html>
<html>
<head>
  <title>Live Stream from ESP32-CAM</title>
</head>
<body>
  <h2>ESP32-CAM Live</h2>
  <img id="stream" width="640">
  <script>
    const ws = new WebSocket('wss://your-server.com/ws'); // Địa chỉ server WebSocket

    ws.onmessage = (event) => {
      const img = document.getElementById('stream');
      img.src = 'data:image/jpeg;base64,' + event.data;
    };
  </script>
</body>
</html>
