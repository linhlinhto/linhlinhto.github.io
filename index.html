<!DOCTYPE html>
<html>
<head>
  <title>ESP32-CAM Stream</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
  <h1>Video Stream</h1>
  <img id="frame" alt="ESP32 Stream Frame">
  
  <script>
    const socket = new WebSocket("wss://0194-171-224-178-50.ngrok-free.app");
    socket.binaryType = "arraybuffer";

    socket.onmessage = function(event) {
      const blob = new Blob([event.data], { type: "image/jpeg" });
      document.getElementById("frame").src = URL.createObjectURL(blob);
    };

    socket.onerror = function(err) {
      console.error("WebSocket Error:", err);
    };

    socket.onclose = () => {
      console.log("❌ WebSocket closed");
    };
  </script>
</body>
</html>
