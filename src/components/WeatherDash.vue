<template>
  <section>
    <h3 class="current">Current Weather</h3>
    <div class="item">
      <h4>{{ Math.ceil(currentWeather.feels_like) }}&#176;</h4>
      <p>{{ currentWeather.weather[0].description }}</p>
      <img :src="generateIconUrl(currentWeather.weather[0].icon)" />
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeatherDash',
  props: ['currentWeather'],
  methods: {
    generateIconUrl(ico) {
      return `http://openweathermap.org/img/wn/${ico}@2x.png`
    }
  }
}
</script>

<style>
section {
  width: 100vw;
}

.item {
  margin: 2px;
  background-color: lightgray;
  width: 200px;
  border: 2px solid gray;
  border-radius: 15px;
  margin: 20px;
}

.current {
  font-family: sans-serif, cursive;
  color: darkgray;
  font-size: 25px;
}
</style>