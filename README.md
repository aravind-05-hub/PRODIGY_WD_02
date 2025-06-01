# PRODIGY_WD_02
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Stopwatch - Prodigy Infotech</title>
  <style>body {
    font-family: Arial, sans-serif;
    background: #121212;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
  }
  
  .container {
    text-align: center;
    background: #1e1e1e;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 0 15px #00ffcc;
  }
  
  #display {
    font-size: 3em;
    margin: 20px 0;
  }
  
  .buttons button {
    padding: 10px 20px;
    margin: 5px;
    font-size: 1em;
    cursor: pointer;
    border: none;
    border-radius: 5px;
    background-color: #00ffcc;
    color: #121212;
  }
  
  #laps {
    list-style: none;
    padding: 0;
    margin-top: 20px;
    text-align: left;
    max-height: 200px;
    overflow-y: auto;
  }
  </style>
</head>
<body>
  <div class="container">
    <h1>Stopwatch</h1>
    <div id="display">00:00:00</div>
    <div class="buttons">
      <button onclick="startStop()">Start</button>
      <button onclick="pause()">Pause</button>
      <button onclick="reset()">Reset</button>
      <button onclick="lap()">Lap</button>
    </div>
    <ul id="laps"></ul>
  </div>

  <script>
    let startTime, updatedTime, difference, timerInterval;
    let running = false;
    let lapCounter = 0;
    
    function updateDisplay(time) {
      const date = new Date(time);
      let minutes = String(date.getUTCMinutes()).padStart(2, '0');
      let seconds = String(date.getUTCSeconds()).padStart(2, '0');
      let milliseconds = String(Math.floor(date.getUTCMilliseconds() / 10)).padStart(2, '0');
      document.getElementById('display').textContent = `${minutes}:${seconds}:${milliseconds}`;
    }
    
    function startStop() {
      if (!running) {
        startTime = new Date().getTime() - (difference || 0);
        timerInterval = setInterval(() => {
          updatedTime = new Date().getTime();
          difference = updatedTime - startTime;
          updateDisplay(difference);
        }, 10);
        running = true;
      }
    }
    
    function pause() {
      clearInterval(timerInterval);
      running = false;
    }
    
    function reset() {
      clearInterval(timerInterval);
      document.getElementById('display').textContent = "00:00:00";
      document.getElementById('laps').innerHTML = "";
      difference = 0;
      running = false;
      lapCounter = 0;
    }
    
    function lap() {
      if (!running) return;
      lapCounter++;
      const li = document.createElement("li");
      li.textContent = `Lap ${lapCounter}: ${document.getElementById('display').textContent}`;
      document.getElementById('laps').appendChild(li);
    }
    </script>
</body>
</html>
