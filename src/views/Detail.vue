<template>
  <div id="weatherDetail" class="py-4">
    <h1 v-if="ready" class="h2 text-custom-primary font-weight-bold d-inline-block">
        {{ weatherData.name }}
    </h1>
    <router-link v-if="ready" to="/" class="close-bt ml-2">X</router-link>
    <b-spinner v-if="!ready" type="grow" class="text-custom-primary loading"></b-spinner>
    <div class="weather-foreacast-data" v-if="ready">
      <b-card class="shadow w-75 mx-auto">
        <b-card-body class="p-0">
          <b-row>
            <b-col sm="4">
            <div v-for="weatherD in weatherData.weather" :key="weatherD.id" class="pt-2">
              <h4>{{ weatherD.main }}</h4>
              <b-img-lazy
                :src="`http://openweathermap.org/img/wn/${weatherD.icon}@2x.png`">
              </b-img-lazy>
              <h5>{{ weatherD.description }}</h5>
            </div>
            </b-col>
            <b-col sm="8" class="text-left pl-4 text-center mt-3 mt-sm-0 text-sm-left">
              <h1 class="text-custom-primary font-weight-bold main-temp">
                {{ Math.round(weatherData.main.temp) }} &deg;C
              </h1>
              <span class="h5 d-block">
                Real Feel : {{ weatherData.main.feels_like }} &deg;C
              </span>
              <span class="h5 d-block">
                Tekanan : {{ weatherData.main.pressure }} bar
              </span>
              <span class="h5 d-block">
                Kelembapan : {{ weatherData.main.humidity }} RH
              </span>
            </b-col>
          </b-row>
        </b-card-body>
      </b-card>
    </div>
  </div>
</template>

<script>
const axios = require('axios').default;

export default {

  data() {
    return {
      ready: false,
      weatherData: null,
    };
  },
  created() {
    this.ready = false;
    this.fetchWeatherData(this.$route.params.lat, this.$route.params.lng);
  },
  methods: {
    fetchWeatherData(lat, lng) {
      axios.get('https://api.openweathermap.org/data/2.5/weather', {
        params: {
          lat,
          lon: lng,
          appid: '191f32fd8cdd0cfd0e9d60f8dc62f239',
          units: 'metric',
        },
      }).then((resp) => {
        if (resp.status === 200) {
          this.weatherData = resp.data;
          this.ready = true;
          console.log(resp);
        } else {
          alert(resp.statusText);
        }
      }).catch((err) => {
        console.log(err);
      });
    },
  },
};

</script>

<style scoped>
  .loading {
    margin: 30px 0;
    width: 80px;
    height: 80px;
  }

  .main-temp {
    font-size: 60px;
  }

  .weather-foreacast-data {
    margin-top: 100px;
  }

  .close-bt {
      cursor: pointer;
      margin-top: -5px;
      background-color: #6C63FF;
      width: 30px;
      height: 30px;
      font-size: 20px;
      text-align: center;
      color: white;
      transition: .1s;
      line-height: 30px;
      border-radius: 15px;
      display: inline-block;
      text-decoration: none;
  }

  .close-bt:hover {
      background-color: rgb(70, 62, 219);
  }

</style>
