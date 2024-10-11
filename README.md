# stopwatch-web-page
A simple and interactive Stopwatch Web Application built using HTML, CSS, and JavaScript. This web app allows users to measure and record time intervals effectively.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Modern Stopwatch</title>
  <style>
    /* General Page Styles */
    body {
      font-family: 'Poppins', sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background: linear-gradient(135deg, #f8b500, #ff7e5f);
    }

    /* Stopwatch Container */
    .stopwatch {
      background: #fff;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
      text-align: center;
      width: 320px;
    }

    /* Display Time */
    .time {
      font-size: 60px;
      margin-bottom: 20px;
      font-weight: bold;
      letter-spacing: 2px;
      color: #333;
    }

    /* Button Styles */
    .buttons button {
      padding: 12px 20px;
      margin: 10px;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease;
      color: white;
    }

    .start {
      background-color: #28a745;
    }

    .pause {
      background-color: #ffc107;
    }

    .reset {
      background-color: #dc3545;
    }

    .lap {
      background-color: #007bff;
    }

    button:hover {
      opacity: 0.9;
    }

    /* Lap Times List */
    .laps {
      margin-top: 20px;
      max-height: 150px;
      overflow-y: auto;
      text-align: left;
    }

    .lap-time {
      background-color: #e9ecef;
      margin: 5px 0;
      padding: 10px;
      border-radius: 5px;
      font-size: 14px;
      color: #555;
    }
  </style>
</head>
<body>

  <!-- Stopwatch Container -->
  <div class="stopwatch">
    <!-- Time Display -->
    <div class="time" id="display">00:00:00</div>
    
    <!-- Buttons -->
    <div class="buttons">
      <button class="start" id="startBtn">Start</button>
      <button class="pause" id="pauseBtn">Pause</button>
      <button class="reset" id="resetBtn">Reset</button>
      <button class="lap" id="lapBtn">Lap</button>
    </div>

    <!-- Lap Times Display -->
    <div class="laps" id="laps"></div>
  </div>

  <script>
    // Variables for Time Tracking
    let hours = 0, minutes = 0, seconds = 0, interval = null, isRunning = false;

    // DOM Elements
    const display = document.getElementById('display');
    const lapsContainer = document.getElementById('laps');

    // Start the Stopwatch
    function startStopwatch() {
      if (!isRunning) {
        interval = setInterval(() => {
          seconds++;
          if (seconds === 60) {
            seconds = 0; minutes++;
          }
          if (minutes === 60) {
            minutes = 0; hours++;
          }
          updateDisplay();
        }, 1000);
        isRunning = true;
      }
    }

    // Pause the Stopwatch
    function pauseStopwatch() {
      clearInterval(interval);
      isRunning = false;
    }

    // Reset the Stopwatch
    function resetStopwatch() {
      clearInterval(interval);
      isRunning = false;
      hours = 0; minutes = 0; seconds = 0;
      updateDisplay();
      lapsContainer.innerHTML = '';
    }

    // Update the Time Display
    function updateDisplay() {
      display.innerHTML = `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
    }

    // Record a Lap Time
    function recordLap() {
      const lapTime = display.innerHTML;
      const lapElement = document.createElement('div');
      lapElement.classList.add('lap-time');
      lapElement.innerText = `Lap: ${lapTime}`;
      lapsContainer.appendChild(lapElement);
    }

    // Event Listeners
    document.getElementById('startBtn').addEventListener('click', startStopwatch);
    document.getElementById('pauseBtn').addEventListener('click', pauseStopwatch);
    document.getElementById('resetBtn').addEventListener('click', resetStopwatch);
    document.getElementById('lapBtn').addEventListener('click', recordLap);
  </script>

</body>
</html>
