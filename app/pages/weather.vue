<template>
  <div class="weather-card">
    <h1 class="app-title">🌤️ WEATHER</h1>
    <v-btn color="primary" @click="getWeatherData" class="fetch-btn">Get Weather Data</v-btn>

    
    <div v-if="currentWeather" class="weather-display">
      
   
      <div class="main-weather-box">
        <h2 class="location-name">{{ currentWeather.location.name }}</h2>
        <div class="hero-weather">
          
          <img :src="`https:${currentWeather.current.condition.icon}`" alt="Weather Icon" class="weather-icon" />
          <div class="temp-condition">
            <span class="main-temp">{{ currentWeather.current.temp_c }}°C</span>
            <p class="condition-text">{{ currentWeather.current.condition.text }}</p>
          </div>
        </div>
      </div>
     
      <div class="details-grid">
  <div class="info-box">
    <v-icon>mdi-weather-partly-cloudy</v-icon>
    <span class="box-value">
      
      {{ currentWeather.forecast.forecastday[0].hour[6].temp_c }}°C
    </span>
    <span class="box-label">6:00 AM</span>
  </div>

  <div class="info-box">
    <v-icon>mdi-weather-partly-cloudy</v-icon>
    <span class="box-value">
        
      {{ currentWeather.forecast.forecastday[0].hour[12].temp_c }}°C
    </span>
    <span class="box-label">12:00 NN</span>
  </div>

  <div class="info-box">
    <v-icon>mdi-weather-partly-cloudy</v-icon>
    <span class="box-value">
        
      {{ currentWeather.forecast.forecastday[0].hour[18].temp_c }}°C
    </span>
    <span class="box-label">6:00 PM</span>
  </div>

  <div class="info-box">
    <v-icon>mdi-weather-partly-cloudy</v-icon>
    <span class="box-value">
        
      {{ currentWeather.forecast.forecastday[0].hour[23].temp_c }}°C
    </span>
    <span class="box-label">11:00 PM</span>
  </div>

        
        <v-btn
        
         color="primary"
        class="refresh-btn"
         block
       prepend-icon="mdi-refresh"
       @click="getWeatherData"
      >
      Refresh Weather
      </v-btn>
        
      </div>

    </div>
  </div>
</template>

<script lang="ts" setup>
//@ts-nocheck
definePageMeta({
  layout: 'weather',
  middleware: 'auth'
})

const currentWeather = ref(null);

const getWeatherData = async () => {
  try {
    const data = await $fetch('http://api.weatherapi.com/v1/forecast.json?key=7b10fac840b443fc93032946262906&q=san fernando&days=4&aqi=no&alerts=no');
    console.log(data);
    currentWeather.value = data;
  } catch (err) {
    console.error("Fetch error:", err);
  }
}

onMounted(getWeatherData);
</script>

<style scoped>
/* Card Wrapper */
.weather-card {
  background-image: url('/image/weather.jpg');
  padding: 25px;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(8px);
  width: 100%;
  max-width: 450px;
  z-index: 10;
}

.app-title {
  font-size: 24px;
  color: #2c3e50;
  margin-bottom: 10px;
}

.fetch-btn {
  margin-bottom: 20px;
}

/* Main Display Container */
.weather-display {
  display: flex;
  flex-direction: column;
  gap: 15px;
}


.main-weather-box {
  background: linear-gradient(135deg, #74b9ff, #0984e3);
  color: white;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 4px 15px rgba(9, 132, 227, 0.3);
}

.location-name {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 10px;
}

.hero-weather {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

.weather-icon {
  width: 80px;
  height: 80px;
  filter: drop-shadow(0px 4px 8px rgba(0,0,0,0.15));
}

.temp-condition {
  text-align: left;
}

.main-temp {
  font-size: 42px;
  font-weight: bold;
  line-height: 1;
}

.condition-text {
  font-size: 16px;
  margin-top: 5px;
  opacity: 0.9;
}

/* Bottom Grid for smaller boxes */
.details-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

/* Individual boxes inside the grid */
.info-box {
  background:linear-gradient(135deg, #74b9ff, #0984e3);
  padding: 15px;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-shadow: white;
  border: 1px solid rgba(0, 0, 0, 0.03);
}

.box-label {
  font-size: 12px;
  color: white;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 4px;
}

.box-value {
  font-size: 16px;
  font-weight: bold;
  color: white;
}

.refresh-btn {
  text-align: center;
  margin-top: 20px;
  border-radius: 10px;
  font-weight: bold;
  text-transform: none;
}
</style>
