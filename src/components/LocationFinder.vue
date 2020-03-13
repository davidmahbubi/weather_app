<template>
  <div id="locationFinder">
    <img src="./../assets/undraw_weather_app_i5sm.svg" class="state-img w-100" alt="Image-state">
    <b-input-group class="mt-5 mx-auto w-50">
        <b-input-group class="mt-3">
            <b-form-input
                placeholder="Cari Lokasi"
                class="find-bt"
                v-model="inputLocation">
            </b-form-input>
            <b-input-group-append>
                <b-button
                    class="btn-outline-custom-primary"
                    @click="fetchLocation(inputLocation)">
                    Cari
                </b-button>
            </b-input-group-append>
        </b-input-group>
    <small class="text-danger text-left mt-1 font-weight-bold" v-if="findRequiredValidate">
        Input wajib diisi
    </small>
    <b-spinner label="Spinning" v-if="loading" class="mx-auto mt-4 text-custom-primary"></b-spinner>
    <div class="search-query-container w-100 mt-3">
        <b-row>
            <b-col
                cols="6"
                class="px-1 mb-2"
                v-for="location in locationList"
                :key="location.formatted"
            >
                <b-card class="search-query-result">
                    <b-card-body class="p-0">
                        <router-link
                            :to="`/detail/${location.geometry.lat}/${location.geometry.lng}`">
                            {{ location.formatted }}
                        </router-link>
                    </b-card-body>
                </b-card>
            </b-col>
        </b-row>
    </div>
    </b-input-group>
  </div>
</template>

<script>

const axios = require('axios').default;

export default {
  data() {
    return {
      inputLocation: null,
      locationList: null,
      loading: false,
    };
  },
  methods: {
    fetchLocation(query) {
      this.locationList = null;
      if (String(query).length > 0) {
        this.loading = true;
        axios.get('https://api.opencagedata.com/geocode/v1/json', {
          params: {
            q: query,
            key: '8ef41d30ac5a45e6b6ab89fbf9a0ba3b',
          },
        })
          .then((resp) => {
            this.locationList = resp.data.results;
            console.log(resp);
          })
          .catch((err) => {
            alert(err);
          })
          .then(() => {
            this.loading = false;
          });
      }
    },
  },
  computed: {
    findRequiredValidate() {
      return String(this.inputLocation).length <= 0;
    },
  },
};
</script>

<style scoped>
  .state-img {
    max-width: 300px;
  }

  .find-bt {
    color: #6C63FF;
    border: 2px solid #6C63FF;
    font-size: 17px;
  }

  .search-query-result {
      border: 2px solid #6C63FF;
  }
</style>
