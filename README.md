# Alarm-clock

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Alarm Clock</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #e8d75c;
        }
        .clock {
            font-size: 3em;
            margin-bottom: 20px;
            font-weight: bold;
        }
        .alarm-section {
            margin-top: 20px;
        }
        input[type="time"] {
            padding: 10px;
            font-size: 16px;
            margin-right: 10px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #6f1e56;
            color: rgb(243, 235, 235);
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: #45a049;
        }
        #alarm-status {
            margin-top: 20px;
            font-size: 1.2em;
            color: #333;
        }
        .alert {
            color: red;
        }
    </style>
</head>
<body>

    <h1>Set Your Alarm</h1>
    
    
    <div class="clock" id="current-time"></div>

    
    <div class="alarm-section">
        <input type="time" id="alarm-time">
        <button onclick="setAlarm()">Set Alarm</button>
    </div>
    
    
    <div id="alarm-status"></div>


    <audio id="alarm-sound" src="https://www.soundjay.com/button/beep-07.wav" preload="auto"></audio>

    <script>
        let alarmTime = null;  
        let alarmSound = document.getElementById("alarm-sound");
        let alarmStatus = document.getElementById("alarm-status");

        
        function updateTime() {
            const currentTime = new Date();
            const hours = String(currentTime.getHours()).padStart(2, '0');
            const minutes = String(currentTime.getMinutes()).padStart(2, '0');
            const seconds = String(currentTime.getSeconds()).padStart(2, '0');
            
        
            document.getElementById("current-time").textContent = `${hours}:${minutes}:${seconds}`;

            
            if (alarmTime && `${hours}:${minutes}` === alarmTime) {
                triggerAlarm();
            }
        }

        
        function setAlarm() {
            const alarmInput = document.getElementById("alarm-time").value;
            if (alarmInput) {
                alarmTime = alarmInput;
                alarmStatus.textContent = `Alarm set for: ${alarmTime}`;
                alarmStatus.classList.remove("alert");
            } else {
                alarmStatus.textContent = "Please set a valid alarm time!";
                alarmStatus.classList.add("alert");
            }
        }

        
        function triggerAlarm() {
            alarmSound.play();
            alarmStatus.textContent = "Time's up! Alarm ringing!";
            alarmStatus.classList.add("alert");
            alarmTime = null;  
        }


        setInterval(updateTime, 1000);
    </script>

</body>
</html>
