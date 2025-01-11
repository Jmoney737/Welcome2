<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Home Dashboard</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            color: white;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            max-width: 1200px;
            padding: 20px;
        }
        .widget {
            background-color: #1e1e1e;
            border: 1px solid #2e7d32;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        .widget h2 {
            font-size: 1.2rem;
            color: #a5d6a7;
        }
        .clock {
            font-size: 3rem;
            font-weight: bold;
        }
        .weather img {
            max-width: 80px;
            margin: 0 auto;
        }
        .button-group {
            display: flex;
            justify-content: space-evenly;
            margin-top: 10px;
        }
        .button-group button {
            background-color: #2e7d32;
            border: none;
            border-radius: 5px;
            color: white;
            padding: 10px 15px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .button-group button:hover {
            background-color: #1b5e20;
        }
        .slider {
            width: 80%;
            margin: 10px auto;
        }
    </style>
</head>
<body>
    <div class="dashboard">
        <!-- Alarm Widget -->
        <div class="widget alarm">
            <h2>Alarm</h2>
            <p id="alarm-status">Armed Home</p>
            <div class="button-group">
                <button onclick="toggleAlarm('arm')">Arm</button>
                <button onclick="toggleAlarm('disarm')">Disarm</button>
            </div>
        </div>
        
        <!-- Clock Widget -->
        <div class="widget clock">
            <h2>Time</h2>
            <div id="time"></div>
            <div id="date"></div>
        </div>

        <!-- Lights Control Widget -->
        <div class="widget lights">
            <h2>Lights</h2>
            <p>Living Room</p>
            <div class="button-group">
                <button onclick="toggleLights('on')">On</button>
                <button onclick="toggleLights('off')">Off</button>
            </div>
            <input type="range" min="0" max="100" value="50" class="slider" id="dimmer" onchange="setBrightness(this.value)">
            <p>Brightness: <span id="brightness-value">50%</span></p>
        </div>

        <!-- Weather Widget -->
        <div class="widget weather">
            <h2>Weather</h2>
            <img id="weather-icon" src="" alt="Weather Icon">
            <p id="weather-data">Loading...</p>
        </div>

        <!-- Hourly Forecast Widget -->
        <div class="widget forecast">
            <h2>Hourly Forecast</h2>
            <ul id="forecast-list" style="list-style: none; padding: 0;"></ul>
        </div>

        <!-- Calendar Widget -->
        <div class="widget calendar">
            <h2>Calendar</h2>
            <p>Upcoming Holidays</p>
            <ul id="calendar-events">
                <li>Loading...</li>
            </ul>
        </div>
    </div>

    <script>
        // Clock Widget
        function updateTime() {
            const now = new Date();
            document.getElementById('time').textContent = now.toLocaleTimeString();
            document.getElementById('date').textContent = now.toLocaleDateString();
        }
        setInterval(updateTime, 1000);
        updateTime();

        // Lights Widget
        function toggleLights(state) {
            console.log(`Lights turned ${state}`);
            alert(`Lights turned ${state}`);
        }
        function setBrightness(value) {
            document.getElementById('brightness-value').textContent = `${value}%`;
            console.log(`Brightness set to ${value}%`);
        }

        // Alarm Widget
        function toggleAlarm(state) {
            const alarmStatus = document.getElementById('alarm-status');
            if (state === 'arm') {
                alarmStatus.textContent = 'Armed Home';
            } else {
                alarmStatus.textContent = 'Disarmed';
            }
            console.log(`Alarm ${state}`);
        }

        // Weather Widget
        fetch('https://api.openweathermap.org/data/2.5/weather?q=New York&appid=your_api_key&units=imperial')
            .then(response => response.json())
            .then(data => {
                document.getElementById('weather-icon').src = `https://openweathermap.org/img/wn/${data.weather[0].icon}.png`;
                document.getElementById('weather-data').textContent = `${data.main.temp}°F, ${data.weather[0].description}`;
            });

        // Hourly Forecast Widget
        fetch('https://api.openweathermap.org/data/2.5/forecast?q=New York&appid=your_api_key&units=imperial')
            .then(response => response.json())
            .then(data => {
                const forecastList = document.getElementById('forecast-list');
                forecastList.innerHTML = '';
                data.list.slice(0, 5).forEach(item => {
                    const li = document.createElement('li');
                    li.textContent = `${new Date(item.dt * 1000).toLocaleTimeString()}: ${item.main.temp}°F, ${item.weather[0].description}`;
                    forecastList.appendChild(li);
                });
            });

        // Calendar Widget (Mock Data for Holidays)
        const holidays = [
            { date: 'Oct 31', name: 'Halloween' },
            { date: 'Nov 24', name: 'Thanksgiving' },
            { date: 'Dec 25', name: 'Christmas' }
        ];
        const calendarEvents = document.getElementById('calendar-events');
        calendarEvents.innerHTML = holidays.map(holiday => `<li>${holiday.date} - ${holiday.name}</li>`).join('');
    </script>
</body>
</html>
