<template>
  <div class="weather-container">
    <div class="weather-wrapper">
      <div class="search-box">
        <input
          v-model="query"
          type="text"
          placeholder="Search by city..."
          class="search-bar"
          @keypress="getWeather"
        >
      </div>

      <div v-if="typeof weather.main != 'undefined'" class="weather-info">
        <div class="location-box">
          <div class="location">
            {{ weather.name }},{{ weather.sys?.country }}
          </div>

          <div class="date">
            {{ currentDate() }}
          </div>
        </div>

        <div class="weather-box">
          <div class="temp">
            {{ Math.round(weather.main.temp) }}°c
          </div>

          <div class="weather">
            {{ weather.weather[0].main }}
          </div>

          <div class="weather-description">
            {{ weather.weather[0].description }}
          </div>

          <div class="more-info">
            <div class="wind-speed">
              wind speed: <span class="value">{{ weather.wind.speed }}</span>&nbsp;mph
            </div>

            <div class="humidity">
              humidity: <br> <span class="value">{{ weather.main.humidity }}</span>%
            </div>

            <div class="pressure">
              pressure: <span class="value">{{ weather.main.pressure }}</span>&nbsp;hPa
            </div>
          </div>
        </div>
      </div>
    </div>
    <footer-comp />
  </div>
</template>

<script>
import FooterComp from '../components/FooterComp.vue'

export default {
  name: 'App',
  components: {
    FooterComp
  },

  data () {
    return {
      api_key: '56ad7118082006e8f85c6b4bff092350',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      weather_icon: 'http://openweathermap.org/img/wn/',
      query: '',
      weather: {}
    }
  },

  methods: {
    getWeather (e) {
      if (e.key === 'Enter') {
        fetch(
    `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then((res) => {
            return res.json()
          })
          .then(this.setData)
      }
    },

    setData (response) {
      this.weather = response
    },

    currentDate () {
      const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
      const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
      const d = new Date()
      const month = months[d.getMonth()]
      const day = days[d.getDay()]
      const date = d.getDate()
      const year = d.getFullYear()
      return `${month} ${date} ${day} ${year}`
    }
  }
}

</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Nanum+Brush+Script&family=Raleway:wght@100&display=swap');

* {
margin: 0;
padding: 0;
box-sizing: border-box;
text-align: center;
color:#fff;
}

body {
background-color: rgb(2, 0, 42);
}

.weather-container{
background-image: url("../assets/default.jpg");
background-size: cover;
background-position: center;
transition: 0.4s;
width: 450px;
margin: 0 auto;
border-radius: 40px;
margin-top: 30px;
box-shadow: 0px 0px 40px #f3f3f365;
font-family: "Raleway";
}

.weather-wrapper {
height: 600px;
padding: 25px;
border-radius: 25px;
background-image: linear-gradient(
to bottom,
rgba(0, 0, 0, 0.2),
rgba(0, 0, 0, 0.4)
);
}

.search-box .search-bar {
display: block;
width: 100%;
padding: 20px;
color: #4c4a4a;
font-size: 1.5rem;
background-color: rgba(255, 255, 255, 0.7);
box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.25);
border-radius: 12px;
transition: 0.5s;
text-align: left;
}

.search-box .search-bar:focus {
box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
background-color: rgba(255, 255, 255, 0.85);
}

.location-box .location {
font-size: 2rem;
font-weight: 500;
margin-top: 30px;
}

.location-box .date {
font-size: 1.2rem;
font-weight: 300;
}

.weather-box .temp {
padding: 10px 25px;
font-size: 6.3rem;
font-weight: 900;
text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
margin: 30px 0px;
}

.weather-box .weather {
font-size: 3rem;
font-weight: 700;
}

.weather-box .weather-description {
font-size: 1.5rem;
font-weight: 500;
}

.more-info {
display: grid;
grid-template-columns: repeat(3, 1fr);
grid-auto-rows: minmax(80px, auto);
font-size: 1rem;
border-radius: 25px;
margin: 30px 0px;
background-color: #d6d6d661;
box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.more-info .value {
  font-size: 1.8rem;
}

.more-info .wind-speed, .humidity, .pressure {
  padding-top: 8px;
}

@media (max-width:580px)  {
  .weather-container {
    width: 95%;
  }
  .more-info {
    font-size: 0.8rem;
  }
}
</style>
