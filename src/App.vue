<template>
  <div id="app">
    <main>
      <div class="weather-all">
        <div class="search-box">
          <input
            type="text"
            class="search-bar"
            placeholder="Search..."
            v-model="query"
            @keypress="fetchWeather"
          />
          <div class="weather-wrap" v-if="weather.main">
            <div class="location-box">
              <div class="location">
                {{ weather.name }}, {{ weather.sys.country }}
              </div>
              <div class="date">{{ dateBuilder() }}</div>
            </div>

            <div class="weather-box">
              <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
              <div class="weather">{{ weather.weather[0].main }}</div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      apikey: "afa2bfc1c58be6612708d71c40cb741a",
      url_base: "http://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key === "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.apikey}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResult);
      }
    },
    setResult(results) {
      this.weather = results;
    },
    dateBuilder() {
      let date = new Date();
      let months = [
        "Ocak",
        "Şubat",
        "Mart",
        "Nisan",
        "Mayıs",
        "Haziran",
        "Temmuz",
        "Ağustos",
        "Eylül",
        "Ekim",
        "Kasım",
        "Aralık",
      ];
      let days = [
        "",
        "Pazartesi",
        "Salı",
        "Çarşamba",
        "Perşembe",
        "Cuma",
        "Cumartesi",
        "Pazar",
      ];
      let day = days[date.getDay()];
      let dates = date.getDate();
      let month = months[date.getMonth()];
      let year = date.getFullYear();

      return `${day} ${dates} ${month} ${year}`;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: Arial, Helvetica, sans-serif;
}
main {
  min-height: 100vh;
  padding: 25px;
}
.weather-all {
  border-radius: 10px;
}
.search-box {
  background: url("./assets/cold-bg.jpeg");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: bottom;
  transition: 0.4s;
  margin: 0 auto;
  width: 289px;
  height: 78vh;
  font-size: 14px;
  margin-bottom: 25px;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 5px 8px 5px 5px #8888887a;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 10px;
  color: #313131;
  font-size: 14px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 8px;
}
.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
}
.location {
  color: rgb(39, 39, 39);
  margin-top: 24px;
  font-size: 18px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.date {
  color: rgb(39, 39, 39);
  margin-top: 10px;
  margin-bottom: 16px;
  font-size: 18px;
  font-weight: 500;
  text-align: center;
  font-style: italic;
}
.weather-box {
  text-align: center;
}
.temp {
  display: inline-block;
  padding: 10px 25px;
  color: rgb(39, 39, 39);
  font-size: 24px;
  font-weight: 900;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather {
  color: rgb(39, 39, 39);
  font-size: 20px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
</style>
