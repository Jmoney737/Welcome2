
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to Our Home</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Great+Vibes&family=Open+Sans:wght@400;600&display=swap');
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Open Sans', sans-serif; line-height: 1.6; color: #333; background-color: #FAF9F6; padding: 20px; }
        header { text-align: center; margin-bottom: 30px; }
        header h1 { font-family: 'Great Vibes', cursive; font-size: 3rem; color: #A88C7D; }
        header p { font-size: 1.2rem; color: #555; }
        .smart-home-link {
            display: inline-block;
            margin-top: 10px;
            padding: 10px 20px;
            background-color: #A88C7D;
            color: #FFF;
            font-weight: bold;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }
        .smart-home-link:hover { background-color: #946b5d; }
        .section { background: #FFF; border-radius: 10px; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); margin-bottom: 20px; padding: 20px; max-width: 800px; margin-left: auto; margin-right: auto; }
        .section h2 { font-family: 'Great Vibes', cursive; font-size: 2rem; color: #A88C7D; margin-bottom: 10px; text-align: center; display: flex; justify-content: space-between; align-items: center; }
        .section-content { display: none; overflow: hidden; transition: max-height 0.3s ease-out, padding 0.3s ease-out; }
        .section-content.active { display: block; }
        ol, ul { text-align: left; }
        img { max-width: 100%; border-radius: 5px; margin: 10px 0; }
        .toggle-btn {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #A88C7D;
            transition: color 0.3s ease;
        }
        .toggle-btn:hover { color: #946b5d; }
    </style>
</head>
<body>
    <header>
        <h1>Welcome to Your Home</h1>
        <p>We’re so glad to have you here. Click on the icons for quick navigation.</p>
        <a href="https://jmoney737.github.io/Routine-Activator/" target="_blank" class="smart-home-link">Smart Home Control</a>
    </header>

    <div class="section">
        <h2>
            Wi-Fi Information 
            <button class="toggle-btn" onclick="toggleSection(this)">▼</button>
        </h2>
        <div class="section-content">
            <ul>
                <li><span>Network Name:</span> KRESS</li>
                <li><span>Password:</span> 9403950691</li>
            </ul>
        </div>
    </div>

    <div class="section">
        <h2>
            Appliances & Devices
            <button class="toggle-btn" onclick="toggleSection(this)">▼</button>
        </h2>
        <div class="section-content">
            <ul>
                <li><span>Thermostat:</span> Don’t Touch.</li>
                <li><span>Smart TV:</span> YouTube TV, Hulu, Netflix, Disney, Prime Video.</li>
                <li>
                    <span>Washer/Dryer:</span> Use the AI Opti Wash & Dry Setting. Detergent is automatically dispensed. Clean filter before use.
                    <a href="#lint-filter-cleaning" style="margin-left: 5px;">See Lint Filter Cleaning Instructions</a>
                </li>
            </ul>
        </div>
    </div>

    <div class="section">
        <h2>
            Nespresso Coffee Preparation Guide
            <button class="toggle-btn" onclick="toggleSection(this)">▼</button>
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

    <div class="section" id="lint-filter-cleaning">
        <h2>
            Lint Filter Cleaning Instructions
            <button class="toggle-btn" onclick="toggleSection(this)">▼</button>
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

    <script>
        function toggleSection(button) {
            const sectionContent = button.parentElement.nextElementSibling;

            // Toggle the active class for visibility
            sectionContent.classList.toggle('active');

            // Change the button text based on the visibility
            if (sectionContent.classList.contains('active')) {
                button.textContent = '▲'; // Collapse icon
            } else {
                button.textContent = '▼'; // Expand icon
            }
        }
    </script>
</body>
</html>
