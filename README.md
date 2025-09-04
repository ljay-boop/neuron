<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            text-align: center;
            background: linear-gradient(to right, #89f7fe, #66a6ff);
            color: #333;
        }
        h1 {
            margin-bottom: 20px;
        }
        form {
            margin-bottom: 20px;
        }
        input {
            padding: 10px;
            font-size: 16px;
        }
        button {
            padding: 10px 15px;
            font-size: 16px;
            background-color: #011cea;
            color: #fff;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        #weather-info {
            margin-top: 20px;
            padding: 20px;
            background: #fff;
            border-radius: 8px;
            display: inline-block;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
    </style>
</head>
<body>
    <h1>Weather App</h1>
    <form id="weather-form">
        <input type="text" id="city" placeholder="Enter city name" required>
        <button type="submit">Get Weather</button>
    </form>
    <div id="weather-info"></div>

    <script>
        const apiKey = '8f606f49304ee7b82c037be6f93ea253'; // Replace with your OpenWeatherMap API key

        document.getElementById('weather-form').addEventListener('submit', async (event) => {
            event.preventDefault();
            const city = document.getElementById('city').value;
            const weatherInfo = document.getElementById('weather-info');

            weatherInfo.innerHTML = '<p>Loading...</p>';
            
            try {
                const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`);
                if (!response.ok) {
                    throw new Error('City not found');
                }
                const data = await response.json();

                weatherInfo.innerHTML = `
                    <h2>${data.name}, ${data.sys.country}</h2>
                    <p>Temperature: ${data.main.temp}°C</p>
                    <p>Weather: ${data.weather[0].description}</p>
                    <p>Humidity: ${data.main.humidity}%</p>
                    <p>Wind Speed: ${data.wind.speed} m/s</p>
                `;
            } catch (error) {
                weatherInfo.innerHTML = `<p>Error: ${error.message}</p>`;
            }
        });
    </script>
</body>
</html>
