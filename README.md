<!DOCTYPE html>
<html>
<head>
  <title>ESP32-CAM Stream</title>
</head>
<body>
  <h1>WebSocket Video Stream</h1>
  <img id="frame" src="" width="640">
  <script>
    const socket = new WebSocket("wss://078f-171-224-178-50.ngrok-free.app/");

    socket.onmessage = function(event) {
      document.getElementById("frame").src = "data:image/jpeg;base64," + event.data;
    };
  </script>
</body>
</html>
