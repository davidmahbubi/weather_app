<template>
  <div id="app">
    <b-row class="weather-container">
      <b-col sm="2" md="3" class="shadow side-nav text-center d-none d-lg-block pt-5 px-lg-0">
        <img src="./assets/undraw_weather_d9t2.svg" class="img-fluid px-5" alt="">
        <h1 class="mt-4 text-custom-primary font-weight-bold">CuacaKu</h1>
        <span class="text-custom-primary text-center w-100 px-3 d-block">
          Aplikasi perkiraan cuaca dengan memanfaatkan OpenWeatherMap API
        </span>
        <span class="text-custom-primary copyright-text">
          <strong>&copy; {{ getYear() }} MHB Project</strong>
        </span>
      </b-col>
      <b-col sm="12" md="9" class="routes-view">
        <router-view/>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  methods: {
    getYear() {
      return new Date().getFullYear();
    },
  },
};
</script>

<style>
#app {
  font-family: 'Baloo 2', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.weather-container {
  height: 100vh;
}

.routes-view {
  height: 100vh;
  overflow: auto;
}

.row {
  margin-left: 0;
  margin-right: 0;
}

.side-nav {
  height: 100%;
}

.text-custom-primary {
  color: #6C63FF;
}

.copyright-text {
  position: absolute !important;
  bottom: 15px;
  right: 0;
  left: 0;
}

.btn-outline-custom-primary {
  border: 2px solid #6C63FF;
  border-left: none;
  color: #6C63FF;
  background-color: rgba(0, 0, 0, 0);
}

.btn-outline-custom-primary:hover, .btn-outline-custom-primary:visited {
  border: 2px solid #6C63FF;
  border-left: none;
  background: #6C63FF;
}

</style>
