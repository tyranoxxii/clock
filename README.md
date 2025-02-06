<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Đồng Hồ Đếm Ngược</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        #timer {
            font-size: 64px;
            font-weight: bold;
            margin-top: 20px;
        }
        button {
            font-size: 18px;
            padding: 10px 20px;
            margin: 10px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Đồng Hồ Đếm Ngược</h1>
    <input type="number" id="inputTime" placeholder="Nhập số giây" />
    <button onclick="startCountdown()">Bắt đầu</button>
    <button onclick="pauseCountdown()">Tạm dừng</button>
    <button onclick="resetCountdown()">Dừng</button>
    <div id="timer">00:00</div>
    <audio id="tickSound" src="https://www.fesliyanstudios.com/play-mp3/4380" preload="auto"></audio>
    
    <script>
        let countdown;
        let seconds;
        let isPaused = false;
        function startCountdown() {
            clearInterval(countdown);
            seconds = document.getElementById("inputTime").value;
            if (!seconds || seconds <= 0) return;
            
            const timerDisplay = document.getElementById("timer");
            const tickSound = document.getElementById("tickSound");
            isPaused = false;
            
            function updateTimer() {
                if (isPaused) return;
                if (seconds <= 0) {
                    clearInterval(countdown);
                    timerDisplay.textContent = "Hết giờ!";
                    return;
                }
                let minutes = Math.floor(seconds / 60);
                let remainingSeconds = seconds % 60;
                timerDisplay.textContent = `${String(minutes).padStart(2, '0')}:${String(remainingSeconds).padStart(2, '0')}`;
                tickSound.play().catch(() => console.log("Âm thanh bị chặn"));
                seconds--;
            }
            
            updateTimer();
            countdown = setInterval(updateTimer, 1000);
        }
        
        function pauseCountdown() {
            isPaused = !isPaused;
        }
        
        function resetCountdown() {
            clearInterval(countdown);
            document.getElementById("timer").textContent = "00:00";
        }
    </script>
</body>
</html>
