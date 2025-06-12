<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Our Home</title>
    <!-- Fonts & FontAwesome -->
    <link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:wght@400;600&family=Open+Sans:wght@400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Open Sans', sans-serif; line-height: 1.6; color: #333; background-color: #FAF9F6; padding: 20px; }
        header { text-align: center; margin-bottom: 30px; }
        header h1 {
            font-family: 'Bodoni Moda', serif;
            font-size: 9rem;
            color: #A88C7D;
        }
        header p { font-size: 1.2rem; color: #555; }
        header a {
            color: #A88C7D;
            font-weight: bold;
            text-decoration: underline;
            font-size: 1.1rem;
        }
        header a:hover {
            color: #946b5d;
        }
        .weather-widget {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: linear-gradient(135deg, #FFF, #F7F2EE);
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 15px;
            margin-bottom: 20px;
        }
        .weather-widget i {
            font-size: 3rem;
            color: #A88C7D;
        }
        .weather-widget div {
            font-size: 1.2rem;
            color: #555;
        }
        .weather-widget div strong {
            color: #A88C7D;
        }
        .search-bar {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }
        .search-bar input {
            padding: 10px;
            font-size: 1rem;
            border: 1px solid #ccc;
            border-radius: 5px 0 0 5px;
            width: 70%;
        }
        .search-bar button {
            padding: 10px 20px;
            font-size: 1rem;
            background-color: #A88C7D;
            color: #FFF;
            border: none;
            border-radius: 0 5px 5px 0;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        .search-bar button:hover { background-color: #946b5d; }
        .divider {
            height: 1px;
            background-color: #ccc;
            margin: 20px 0;
        }
        .section {
            background: linear-gradient(135deg, #FFF, #F7F2EE);
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            padding: 20px;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
        }
        .section h2 {
            font-family: 'Bodoni Moda', serif;
            font-size: 2rem;
            color: #A88C7D;
            margin-bottom: 10px;
            text-align: center;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .section-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out, padding 0.3s ease-out;
        }
        .section-content.active {
            max-height: 1000px;
            padding: 10px 0;
        }
        .drawer-button {
            margin: 5px;
            padding: 8px 16px;
            border: none;
            background: #A88C7D;
            color: #fff;
            border-radius: 5px;
            font-size: 1rem;
            cursor: pointer;
            transition: background 0.3s;
        }
        .drawer-button:hover { background: #946b5d; }
        img {
            max-width: 100%;
            height: auto;
            border-radius: 7px;
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to Our Home</h1>
        <p>We’re so glad to have you here. Click on the icons for quick navigation.</p>
        <p>
            <a href="http://192.168.68.151:8123" target="_blank">
                Smart Home Control
            </a>
        </p>
    </header>

<!-- Weather Widget -->
<div class="weather-widget" id="weather-widget">
    <i class="fas fa-cloud-sun"></i>
    <div id="weather-data">
        <p>Loading weather data...</p>
    </div>
    <div id="forecast" class="forecast">
        <!-- Forecast will be dynamically populated here -->
    </div>
</div>

<script>
    async function fetchWeather() {
        const apiKey = '7841816e864c04d9b862cb645522ca43';
        const city = 'Denton';
        const weatherUrl = `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=imperial&appid=${apiKey}`;
        const forecastUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${city}&units=imperial&appid=${apiKey}`;
        const weatherDataDiv = document.getElementById('weather-data');
        const forecastDiv = document.getElementById('forecast');

        try {
            // Fetch current weather
            const weatherResponse = await fetch(weatherUrl);
            if (!weatherResponse.ok) throw new Error('Weather data not found');
            const weatherData = await weatherResponse.json();

            weatherDataDiv.innerHTML = `
                <p><strong>City:</strong> ${weatherData.name}</p>
                <p><strong>Temperature:</strong> ${weatherData.main.temp} &deg;F</p>
                <p><strong>Weather:</strong> ${weatherData.weather[0].description}</p>
                <p><strong>Humidity:</strong> ${weatherData.main.humidity}%</p>
                <p><strong>Wind Speed:</strong> ${weatherData.wind.speed} mph</p>
            `;

            // Fetch 5-day forecast
            const forecastResponse = await fetch(forecastUrl);
            if (!forecastResponse.ok) throw new Error('Forecast data not found');
            const forecastData = await forecastResponse.json();

            // Process forecast data for every 8th timestamp (every 24 hours)
            const dailyForecasts = forecastData.list.filter((_, index) => index % 8 === 0);
            forecastDiv.innerHTML = `
                <h3>5-Day Forecast</h3>
                <ul>
                    ${dailyForecasts
                        .map((day) => {
                            const date = new Date(day.dt * 1000);
                            const options = { weekday: 'long', month: 'short', day: 'numeric' };
                            return `
                                <li>
                                    <strong>${date.toLocaleDateString('en-US', options)}</strong>
                                    <p>Temp: ${day.main.temp} &deg;F</p>
                                    <p>Weather: ${day.weather[0].description}</p>
                                </li>
                            `;
                        })
                        .join('')}
                </ul>
            `;
        } catch (error) {
            weatherDataDiv.innerHTML = `<p>Error fetching weather data: ${error.message}</p>`;
        }
    }

    window.onload = fetchWeather;

    function toggleSection(button, sectionId = null) {
        // Identify the section content to toggle
        const sectionContent = sectionId 
            ? document.querySelector(`#${sectionId} .section-content`) 
            : button.closest('.section').querySelector('.section-content');

        // Check if the section is already active
        const isActive = sectionContent.classList.contains('active');

        // Collapse all other sections
        document.querySelectorAll('.section-content').forEach(content => {
            content.classList.remove('active');
            content.style.maxHeight = null;
        });

        // Expand the clicked section if it was not active
        if (!isActive) {
            sectionContent.classList.add('active');
            sectionContent.style.maxHeight = sectionContent.scrollHeight + 'px';
        }
    }

    function toggleDrawer(drawerId) {
        const drawer = document.getElementById(drawerId);
        const isActive = drawer.classList.contains('active');

        // Collapse all other drawers and cabinets
        document.querySelectorAll('.section-content').forEach(content => {
            content.classList.remove('active');
            content.style.maxHeight = null;
        });

        // Expand the clicked drawer or cabinet if it was not active
        if (!isActive) {
            drawer.classList.add('active');
            drawer.style.maxHeight = drawer.scrollHeight + 'px';
        }
    }

    function searchSections() {
        const query = document.getElementById('search-input').value.toLowerCase();
        document.querySelectorAll('.section').forEach(section => {
            const text = section.textContent.toLowerCase();
            if (text.includes(query)) {
                section.style.display = '';
            } else {
                section.style.display = 'none';
            }
        });
    }
</script>

    <!-- Search Bar -->
    <div class="search-bar">
        <input type="text" id="search-input" placeholder="Search for a section..." aria-label="Search for a section">
        <button onclick="searchSections()">Search</button>
    </div>

    <div class="divider"></div>

    <!-- Example Section -->
    <div class="section" id="appliances">
        <h2>
            <i class="fas fa-tv"></i> Appliances & Devices
            <button class="toggle-btn" onclick="toggleSection(this, 'appliances')" aria-label="Toggle section">
                <i class="fas fa-chevron-down"></i>
            </button>
        </h2>
        <div class="section-content">
            <ul>
                <li><strong>Thermostat:</strong> Don’t Touch.</li>
                <li><strong>Smart TV:</strong> YouTube TV, Hulu, Netflix, Disney, Prime Video.</li>
                <li>
                    <strong>Washer/Dryer:</strong> Use the AI Opti Wash & Dry Setting. Detergent is automatically dispensed. Clean filter before use.
                    <a href="#lint-filter-cleaning" style="margin-left: 5px;">See Lint Filter Cleaning Instructions</a>
                </li>
            </ul>
        </div>
    </div>
    
    <div class="divider"></div>

    <!-- Nespresso Coffee Preparation Guide -->
    <div class="section">
        <h2>
            <i class="fas fa-coffee"></i> Nespresso Coffee Preparation Guide
            <button class="toggle-btn" onclick="toggleSection(this)">
                <i class="fas fa-chevron-down"></i>
            </button>
        </h2>
        <div class="section-content">
            <ol>
                <p><strong>Note:</strong> Capsules are to the left in the jar. The automatic motor raises and lowers the machine's head when the lever is pushed up or down.</p>
                <li>Fill the water tank with fresh drinking water.</li>
                <img src="https://github.com/user-attachments/assets/b2e02e7d-1c8a-4cee-84ad-52ac8514c588" alt="Fill Water Tank">
                <li>Turn on the machine by pressing the button.</li>
                <img src="https://github.com/user-attachments/assets/797a5710-f9b1-4916-a2c6-cb403407c967" alt="Machine Button">
                <li>GREEN lights will blink while the machine is heating up.</li>
                <img src="https://github.com/user-attachments/assets/4472e73a-19de-4921-9d1b-0a32f4deea4a" alt="Heating Indicator">
                <li>Steady GREEN light indicates the machine is ready.</li>
                <img src="https://github.com/user-attachments/assets/f9577087-ca37-42a7-9068-29e00fcad0f8" alt="Ready Light">
                <li>Place a cup under the coffee outlet.</li>
                <img src="https://github.com/user-attachments/assets/1abf0322-36b9-47ab-8629-199779d02c84" alt="Place Cup">
                <li>Open the machine head by pushing the lever up.</li>
                <img src="https://github.com/user-attachments/assets/03cb69aa-3172-47e4-9511-84bfad7a0fc4" alt="Open Machine Head">
                <li>Insert a capsule, dome side down.</li>
                <li>Close the lid by pressing the lever down, then press the button to start brewing.</li>
            </ol>
        </div>
    </div>

    <div class="divider"></div>

    <!-- Lint Filter Cleaning Instructions -->
    <div class="section" id="lint-filter-cleaning">
        <h2>
            <i class="fas fa-filter"></i> Lint Filter Cleaning Instructions
            <button class="toggle-btn" onclick="toggleSection(this)">
                <i class="fas fa-chevron-down"></i>
            </button>
        </h2>
        <div class="section-content">
            <ol>
                <li>Open the lint filter cover and pull out the lint filter.</li>
                <img src="https://github.com/user-attachments/assets/26512380-ef32-44d5-ae12-3c88316588c6" alt="Lint Filter Cover">
                <li>Avoid removing the rubber seal on the filter.</li>
                <img src="https://github.com/user-attachments/assets/18dacdf1-a21b-4aef-8b52-3ed60f90d134" alt="Rubber Seal">
                <li>Separate the outer and inner filters.</li>
                <img src="https://github.com/user-attachments/assets/2c1c4ce0-a6c2-4c5a-9e40-c09a6d7b2394" alt="Separate Filters">
                <li>Remove lint from both filters.</li>
                <li>Reassemble the filters and insert them back in place.</li>
            </ol>
        </div>
    </div>

    <div class="divider"></div>

    <!-- Guide to Local Bars and Restaurants -->
    <div class="section">
        <h2>
            <i class="fas fa-utensils"></i> Guide to Local Bars and Restaurants
            <button class="toggle-btn" onclick="toggleSection(this)" aria-label="Toggle section">
                <i class="fas fa-chevron-down"></i>
            </button>
        </h2>
        <div class="section-content">
            <ul>
                <li>
                    <strong>GreenHouse Restaurant and Bar</strong><br>
                    Enjoy New American cuisine and an award-winning bar. 
                    <a href="https://greenhouserestaurantdenton.com/" target="_blank">Visit Website</a>
                </li>
                <li>
                    <strong>Rooster's Roadhouse</strong><br>
                    Casual BBQ and burgers in a relaxed atmosphere. 
                    <a href="https://roosters-roadhouse.com/" target="_blank">Visit Website</a>
                </li>
                <li>
                    <strong>Barley & Board</strong><br>
                    A gastropub with craft beers and elevated comfort food. 
                    <a href="https://www.barleyandboard.com/" target="_blank">Visit Website</a>
                </li>
            </ul>
        </div>
    </div>

    <div class="divider"></div>

    <!-- Local Attractions -->
    <div class="section">
        <h2>
            <i class="fas fa-map-marker-alt"></i> Local Attractions
            <button class="toggle-btn" onclick="toggleSection(this)" aria-label="Toggle section">
                <i class="fas fa-chevron-down"></i>
            </button>
        </h2>
        <div class="section-content">
            <ul>
                <li>
                    <strong>Denton Courthouse-on-the-Square Museum</strong><br>
                    Learn about local history in this iconic courthouse. 
                    <a href="https://dentoncounty.gov/Departments/Courthouse-on-the-Square" target="_blank">Visit Website</a>
                </li>
                <li>
                    <strong>Ray Roberts Lake State Park</strong><br>
                    A haven for nature enthusiasts with hiking, biking, and fishing. 
                    <a href="https://tpwd.texas.gov/state-parks/ray-roberts-lake" target="_blank">Visit Website</a>
                </li>
                <li>
                    <strong>Arts & Jazz Festival</strong><br>
                    An annual festival featuring live music, art, and local food. 
                    <a href="https://dentonjazzfest.com/" target="_blank">Visit Website</a>
                </li>
            </ul>
        </div>
    </div>

    <div class="divider"></div>

<!-- Combined Section for Drawers and Cabinets -->
<div class="section">
    <h2>
        <i class="fas fa-archive"></i> Office Storage
    </h2>
    <div class="drawer-buttons">
        <button class
