# PRODIGY_WD_02
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STOP WATCH</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .stopwatch {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 30px;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        #display {
            font-size: 4em;
            margin-bottom: 30px;
            font-weight: bold;
            color: #00ff88;
            text-shadow: 0 0 20px rgba(0, 255, 136, 0.5);
            font-family: 'Courier New', monospace;
        }

        .buttons {
            display: flex;
            gap: 15px;
            justify-content: center;
        }

        button {
            padding: 15px 30px;
            font-size: 1.2em;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        #start {
            background: linear-gradient(45deg, #00ff88, #00cc6a);
            color: white;
        }

        #start:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 255, 136, 0.4);
        }

        #stop {
            background: linear-gradient(45deg, #ff4757, #ff3742);
            color: white;
        }

        #stop:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 71, 87, 0.4);
        }

        #reset {
            background: linear-gradient(45deg, #74b9ff, #0984e3);
            color: white;
        }

        #reset:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(116, 185, 255, 0.4);
        }

        button:active {
            transform: translateY(0);
        }
    </style>
</head>
<body>
    <div class="stopwatch">
        <h1>STOP WATCH</h1>
        <div id="display">00:00:00</div>
        <div class="buttons">
            <button id="start">Start</button>
            <button id="stop">Stop</button>
            <button id="reset">Reset</button>
        </div>
    </div>

    <script>
        const display = document.getElementById('display');
        const startButton = document.getElementById('start');
        const stopButton = document.getElementById('stop');
        const resetButton = document.getElementById('reset');

        let timer = null;
        let startTime = 0;
        let elapsedTime = 0;
        let isRunning = false;

        function formatTime(milliseconds) {
            const totalSeconds = Math.floor(milliseconds / 1000);
            const minutes = Math.floor(totalSeconds / 60);
            const seconds = totalSeconds % 60;
            const ms = Math.floor((milliseconds % 1000) / 10); // Get centiseconds

            return ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}:${ms.toString().padStart(2, '0')};
        }

        function updateDisplay() {
            const currentTime = Date.now();
            elapsedTime = currentTime - startTime;
            display.textContent = formatTime(elapsedTime);
        }

        function start() {
            if (!isRunning) {
                startTime = Date.now() - elapsedTime;
                timer = setInterval(updateDisplay, 10); // Update every 10ms for smooth animation
                isRunning = true;
                startButton.textContent = 'Resume';
            }
        }

        function stop() {
            if (isRunning) {
                clearInterval(timer);
                isRunning = false;
                startButton.textContent = 'Resume';
            }
        }

        function reset() {
            clearInterval(timer);
            isRunning = false;
            elapsedTime = 0;
            startTime = 0;
            display.textContent = '00:00:00';
            startButton.textContent = 'Start';
        }

        // Event listeners
        startButton.addEventListener('click', start);
        stopButton.addEventListener('click', stop);
        resetButton.addEventListener('click', reset);
    </script>
</body>
</html>
