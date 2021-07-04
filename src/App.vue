<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" v-model="query" @keypress.enter="fetchWeather" placeholder="manila, ph">
      </div> 
      
      <div class="weather" v-if=" typeof weather.main != 'undefined' ">
        <div class="location">
          {{ weather.name }} {{ weather.sys.country }}
        </div>
        <div class="temperature">
          {{ weather.main.temp }} &deg;c
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      api_key : '242ad9a364fdb6148549142fa3acc632',
      openWeatherMap: 'https://api.openweathermap.org/data/2.5/weather',
      weather: {},
      query: '',
    }
  },
  mounted(){
    this.query = "Bataan, ph"
    this.fetchWeather()
  },
  methods:{
    fetchWeather(){
      fetch(`${this.openWeatherMap}?q=${this.query}&units=metric&APPID=${this.api_key}`)
      .then(res => res.json())
      .then(data => this.weather = data)
    }
  }
}
</script>

<style>
#app {
  
}
</style>
