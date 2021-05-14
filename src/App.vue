<template>
  <div id="app">
    <div id="map">
    </div>
    <markers-list/>
  </div>
</template>

<script>
import MarkersList from '@/components/MarkersList';
export default {
  components: {
    MarkersList
  },
  mounted() {
    var map = L.map('map').setView([50, 70], 3);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);
  }
}
</script>

<style lang="scss" scoped>
#app {
  font-family: 'Roboto', sans-serif;
}
#map {
  width: 80%;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
}
</style>
