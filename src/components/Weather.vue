<template>
  <div id="weather-app">
    <div class="input-form">
      <div class="title-input-form"> 
        <h1>Your Location</h1>
        <p class="text-center"> to know your location weather</p>
      </div>
      <div class="type-input-form">
        <form class="search-location" v-on:submit.prevent="getWeather">
        <input
          type="text"
          class="main-input-form"
          placeholder="What City?"
          v-model="citySearch"
          autocomplete="off"
        />
      </form>
      <p v-if="cityFound">no city found</p>
      </div>
    </div>
    <div class="weather-info">
      <div class="temp-info" v-if="isVisible">
        <h1>{{ weather.temperature }}&deg;C</h1>
        <img src="@/assets/images/cloudy_pink.png" alt="Gambar Awan" width="100px">
        <p>{{ weather.description }}</p>
        <h1>{{ weather.cityName }}</h1>
      </div>
      <div class="out-temp-info" v-if="isVisible"> 
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

      // for loop number
      timeUse: 0,
      timeFast: 15,
      timeSlow: 50,
      timeVerySlow: 85,
      timeFastPress: 5,
      timeSlowPress: 10,
      timeVerySlowPress: 35,

      // visible
      cityFound: false,
      isVisible: false,

      citySearch: "",
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
  methods: {
    getWeather: async function(){
      
      let tempTemp      = 0,
          tempPressure  = 0,
          tempHumidity  = 0,
          tempWind      = 0;
      
      console.log(tempTemp, tempPressure, tempHumidity, tempWind);

      console.log(this.citySearch);
      const apikey = "d87e5a69083c85109cf537d455349cf8";
      const baseURL = `http://api.openweathermap.org/data/2.5/weather?q=${this.citySearch}&appid=${apikey}&units=metric`;

      this.weather.temperature = 0;
      this.weather.pressure = 0;
      this.weather.wind = 0.0;
      this.weather.humidity = 0;

      try {
        const response = await fetch(baseURL);
        const data = await response.json();
        console.log(data);
        this.citySearch = "";

        this.weather.cityName = data.name;
        this.weather.description = data.weather[0].description;

        tempTemp = Math.round(data.main.temp);
        this.timeUse = 0;
        this.countUpTemp(tempTemp);

        tempPressure = data.main.pressure;
        this.timeUse = 0;
        this.countUpPressure(tempPressure);

        tempHumidity = data.main.humidity;
        this.timeUse = 0;
        this.countUpHumidity(tempHumidity);

        tempWind = data.wind.speed;
        this.timeUse = 0;
        this.countUpWind(tempWind);

        this.isVisible = true;
        this.cityFound = false;

      } catch (error) {
        console.log(error);
        this.isVisible = false;
        this.cityFound = true;
      }
      
    },

    countUpTemp: function(realTemp){
      
      console.log(this.timeUse, realTemp);
      if(this.weather.temperature < realTemp - 10){
        this.timeUse = this.timeFast
      }else if(this.weather.temperature > realTemp - 10 && this.weather.temperature < realTemp - 3){
        this.timeUse = this.timeSlow;
      }else{
        this.timeUse = this.timeVerySlow;
      }

      setTimeout(() =>{
        if(this.weather.temperature < realTemp){
          this.weather.temperature += 1;
          this.countUpTemp(realTemp);
        }
      }, this.timeUse);
      
    },

    countUpPressure: function(realTemp){
      
      if(this.weather.pressure < realTemp - 50){
        this.timeUse = this.timeFastPress
      }else if(this.weather.pressure > realTemp - 50 && this.weather.pressure < realTemp - 10){
        this.timeUse = this.timeSlowPress;
      }else{
        this.timeUse = this.timeVerySlowPress;
      }

      setTimeout(() =>{
        if(this.weather.pressure < realTemp){
          this.weather.pressure += 1;
          this.countUpPressure(realTemp);
        }
      }, this.timeUse);
      
    },

    countUpHumidity: function(realTemp){
      
      if(this.weather.humidity < realTemp - Math.round(realTemp/2)){
        this.timeUse = this.timeFast
      }else if(this.weather.humidity > realTemp - Math.round(realTemp/2) && this.weather.humidity < realTemp - Math.round(realTemp/3)){
        this.timeUse = this.timeSlow;
      }else{
        this.timeUse = this.timeVerySlow;
      }

      setTimeout(() =>{
        if(this.weather.humidity < realTemp){
          this.weather.humidity += 1;
          this.countUpHumidity(realTemp);
        }
      }, this.timeUse);
      
    },

    countUpWind: function(realTemp){
      let temp = this.weather.wind;
      temp = parseFloat(temp);

      if(this.weather.wind < realTemp - Math.round(realTemp/8)){
        this.timeUse = this.timeFast
      }else if(this.weather.wind > realTemp - Math.round(realTemp/8) && this.weather.wind < realTemp - Math.round(realTemp/10)){
        this.timeUse = this.timeSlow;
      }else{
        this.timeUse = this.timeVerySlow;
      }

      setTimeout(() =>{
        if(temp < parseFloat(realTemp)){
          temp += 0.01;
          temp = parseFloat(temp).toFixed(2);
          this.weather.wind = temp;
          
          this.countUpWind(realTemp);
        }
      }, this.timeUse);
      
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "../assets/styles/weather.css";
</style>
