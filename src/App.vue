<template>
  <div id="app" :class="typeof weather.main != 'undefined' && isCloudy() ? 'clouds' : ''">
    <main>
      <div class="search-box">
        <input 
          class="search-bar"
          type="text"
          placeholder="Search location"
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ getFormattedDate() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}° C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      api_key: "531906a27b568b0383244c3061bde4c9",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      if(e.key == "Enter") {
        if(this.query.length > 0) {
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
            .then(res => {
              return res.json();
            })
            .then(this.setResults);
        }
        
      }
    },
    setResults(results) {
      if(results.message == undefined) {
        this.weather = results;
        this.query = "";
      }
      console.log(results);
    },
    isCloudy() {
      if ("Clouds" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Rain" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Thunderstorm" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Drizzle" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Snow" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Mist" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Smoke" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Haze" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Dust" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Fog" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Sand" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Ash" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Squall" == this.weather.weather[0].main) {
        return true;
      }
      else if ("Tornado" == this.weather.weather[0].main) {
        return true;
      }
      else{
        return false;
      }
    },
    isSnowing() {
      return false;
    },
    getFormattedDate() {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day}, ${month} ${date}, ${year}`;
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/clear-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.5s;
}

#app.clouds {
  background-image: url('./assets/clouds-bg.webp');
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.25));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  border-radius: 0px 15px 0px 15px;
  color: #313131;
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255,255,255,0.5);
  transition: 0.5s;
}

.search-box .search-bar:focus {
  background-color: rgba(255,255,255,0.75);
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
  border-radius: 15px 0px 15px 0px;
}

.location-box .location {
  color: #ffffff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.location-box .date {
  color: #ffffff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #ffffff;
  font-weight: 900;
  font-size: 102px;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 15px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}

.weather-box .weather {
  color: #ffffff;
  font-weight: 700;
  font-size: 48px;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
}
</style>
