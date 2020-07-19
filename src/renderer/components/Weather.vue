<template>
<div class="weather" style="position: absolute; top: 0%; right: 0%; text-align: right; font-size: 300%">
      <p>{{City}}</p>
      <p>{{Temp}}&deg;C</p>
      <v-img :src="`${firstHalf+weatherIcon+lastHalf}`"></v-img>
    </div>
</template>

<script>
export default {
  data: () => ({
    City: null,
    Temp: null,
    firstHalf: 'http://openweathermap.org/img/wn/',
    weatherIcon: '',
    lastHalf: '@2x.png'
  }),
  methods: {
      refreshWeather() {
          var date = new Date();
      var minutes = date.getMinutes();
      var seconds = date.getSeconds();
      if (minutes % 5 == 0 && seconds == 0) {
        this.startWeather(2644668);
      }
      setTimeout(this.refreshWeather, 1000);
      },
    startWeather(cityID) {
      var key = "5f88303049ce762c6f22f7a4da73600a";
      let self = this;
      fetch(
        "https://api.openweathermap.org/data/2.5/weather?id=" +
          cityID +
          "&appid=" +
          key
      )
        .then(function(resp) {
          return resp.json();
        })
        .then(function(data) {
          console.log(data);
          self.City = data.name;
          self.Temp = Math.round(parseFloat(data.main.temp) - 273.15);
          self.weatherIcon = data.weather[0].icon;
          self.Wind =
            "Wind speed " +
            data.wind.speed +
            " Wind direction " +
            data.wind.deg;
          
        });
    }
  },
  mounted() {
      this.startWeather(2644668);
  }
};
</script>