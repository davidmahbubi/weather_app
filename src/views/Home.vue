<template>
  <div class="home py-4">
    <h1 class="h2 text-custom-primary font-weight-bold">Pilih Lokasi</h1>
    <div class="weather-state-container mt-5">
      <location-finder v-if="!location"></location-finder>
    </div>
    <img src="" alt="">
  </div>
</template>

<script>

import LocationFinder from '@/components/LocationFinder.vue';

export default {
  name: 'Home',
  components: {
    LocationFinder,
  },
  data() {
    return {
      location: null,
    };
  },
};
</script>

<style scoped>

</style>
