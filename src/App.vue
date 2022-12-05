<template>
  <div id="app">
    <WeatherDash v-if="currentWeather" :currentWeather='currentWeather'/>
    <WeeklyForecast v-if="dailyWeather" :dailyWeather='dailyWeather'/>

    <div v-else>
      <h3>No Weather Data</h3>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import WeatherDash from './components/WeatherDash.vue'
  import WeeklyForecast from './components/WeeklyForecast.vue'
  const API_KEY = process.env.VUE_APP_WEATHER_KEY
  export default {
    name: 'App',
    components: {
      WeatherDash,
      WeeklyForecast
    },
    data: () => ({
      dailyWeather: [],
      currentWeather: null
    }),
    mounted: function() {
      navigator.geolocation.getCurrentPosition(async (position) => {
        await this.getCurrentWeather(position.coords)
      })
    },
    methods: {
      async getCurrentWeather(coords) {
        const response = await axios.get(`https://api.openweathermap.org/data/2.5/onecall?lat=${coords.latitude}&lon=${coords.longitude}&units=imperial&appid=${API_KEY}`)
        this.currentWeather = response.data.current
        response.data.daily.splice(0,1)
        this.dailyWeather = response.data.daily
      }
    }
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
