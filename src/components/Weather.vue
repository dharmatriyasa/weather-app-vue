<template>
  <div id="weather-app">
    <div class="input-form">
      <div class="title-input-form"> 
        <h1 class="title text-center">Your Location</h1>
        <p class="text-center"> to know your location weather</p>
      </div>
      <div class="type-input-form">
        <form class="search-location" v-on:submit.prevent="getWeather">
        <input
          type="text"
          class="form-control text-muted form-rounded p-4 shadow-sm"
          placeholder="What City?"
          v-model="citySearch"
          autocomplete="off"
        />
      </form>
      </div>
    </div>
    <div class="weather-info">
      <div class="temp-info">
        <h1>{{ weather.temperature }}&deg;C</h1>
        <img src="@/assets/images/cloudy.png" alt="Gambar Awan" width="100px">
        <p>{{ weather.description }}</p>
        <h1>{{ weather.cityName }}</h1>
        
        
      </div>
      <div class="out-temp-info"> 
        <div class="template-out-temp-info">
          <h2 class="title-toti">Humidity</h2>
          <h2 class="value-toti">{{ weather.humidity }}%</h2>
        </div>
        <div class="template-out-temp-info">
          <h2 class="title-toti">Pressure</h2>
          <h2 class="value-toti">{{ weather.pressure }}&deg;</h2>
        </div>
        <div class="template-out-temp-info">
          <h2 class="title-toti">Wind</h2>
          <h2 class="value-toti">{{ weather.wind }}<span class="small-value-toti">mph</span></h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Weather',
  props: {
    msg: String
  },
  data(){
    return {
      weather: {
        cityName: "Bali",
        country: "ID",
        temperature: 17,
        description: "Clouds everywhere",
        pressure: 95,
        humidity: "44",
        wind: 1.5
      },
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "../assets/styles/weather.css";
</style>
