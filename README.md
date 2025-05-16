<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8">
  <title>Weer Dashboard Nederland & België</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #eef1f5;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
      margin-top: 30px;
    }
    .card {
      background: white;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    .location {
      font-weight: bold;
      margin-bottom: 10px;
      font-size: 1.2em;
    }
    .weather {
      font-size: 1.1em;
    }
  </style>
</head>
<body>

<h1>Weer Nederland & België</h1>

<div class="grid">
  <div class="card" id="weather-nl-north"></div>
  <div class="card" id="weather-nl-south"></div>
  <div class="card" id="weather-be-flanders"></div>
  <div class="card" id="weather-be-wallonia"></div>
</div>

<script>
  const apiKey = "c078e3a0dcb9f7a046398ed9ca4da3b4";

  const locations = [
    { id: "weather-nl-north", name: "Noord Nederland (Groningen)", lat: 53.2194, lon: 6.5665 },
    { id: "weather-nl-south", name: "Zuid Nederland (Eindhoven)", lat: 51.4416, lon: 5.4697 },
    { id: "weather-be-flanders", name: "Vlaanderen (Gent)", lat: 51.0536, lon: 3.7304 },
    { id: "weather-be-wallonia", name: "Wallonië (Namen)", lat: 50.4669, lon: 4.8674 }
  ];

  locations.forEach(loc => {
    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${loc.lat}&lon=${loc.lon}&units=metric&lang=nl&appid=${apiKey}`)
      .then(res => res.json())
      .then(data => {
        document.getElementById(loc.id).innerHTML = `
          <div class="location">${loc.name}</div>
          <div class="weather">
            🌡️ Temperatuur: ${data.main.temp}°C<br>
            💧 Vochtigheid: ${data.main.humidity}%<br>
            🌬️ Wind: ${data.wind.speed} m/s<br>
            🌤️ ${data.weather[0].description}
          </div>
        `;
      })
      .catch(err => {
        document.getElementById(loc.id).innerHTML = `<p>Kon het weer niet laden voor ${loc.name}</p>`;
      });
  });
</script>

</body>
</html>
