<template>
  <div class="container mt-5">
    <div class="form-group">
      <label for="place">Введите место:</label>
      <input v-model="place" type="text" class="form-control" id="place" placeholder="Место" />
    </div>
    <button @click="getWeather" class="btn btn-primary">Узнать погоду</button>

    <div v-if="weatherData" class="mt-4">
      <h3>Погода в {{ place }}</h3>
      <p>Температура: {{ weatherData.main.temp }} °C</p>
      <p>Температура ощущается как: {{ weatherData.main.feels_like }} °C</p>
      <p>Минимальная температура: {{ weatherData.main.temp_min }} °C</p>
      <p>Максимальная температура: {{ weatherData.main.temp_max }} °C</p>
      <p>Уровень облачности: {{ weatherData.clouds.all }}%</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      place: '',
      weatherData: null,
    };
  },
  methods: {
    async getWeather() {
      if (!this.place) {
        alert('Введите место');
        return;
      }
      const api_key = ``;
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.place}&units=metric&appid=${api_key}`;

      try {
        const response = await fetch(url);
        if (!response.ok) {
          throw new Error('Место не найдено.');
        }
        const data = await response.json();
        this.weatherData = data; 
      } catch (error) {
        alert(error.message);
      }
    },
  },
};
</script>