<template>
  <div id="app">
    <div id="map">
    </div>
    <markers-list
    :markers="markers" />
  </div>
</template>

<script>
import MarkersList from '@/components/MarkersList';
import markers from '@/assets/markers.json';

export default {
  components: {
    MarkersList
  },
  data() {
    return {
      markers: markers,
      isMarkerIsYellow: false,
    }
  },
  methods: {
    loadingMarkersOnTheMap(map) {
      const LeafIcon = L.Icon.extend({
        options: {
          iconSize: [38, 95],
          shadowSize: [50, 64],
          iconAnchor: [22, 94],
          shadowAnchor: [4, 62],
          popupAnchor: [-3, -76]
        }
      });

      const greenIcon = new LeafIcon({
        iconUrl: 'http://leafletjs.com/examples/custom-icons/leaf-green.png',
        shadowUrl: 'http://leafletjs.com/examples/custom-icons/leaf-shadow.png'
      });

      const yellowIcon = new LeafIcon({
        iconUrl: 'https://leafletjs.com/examples/custom-icons/leaf-orange.png',
        shadowUrl: 'http://leafletjs.com/examples/custom-icons/leaf-shadow.png'
      });
      
      this.markers.forEach( (currentValue) => {
        let currentMarker = L.marker([currentValue.latitude, currentValue.longitude], {icon: greenIcon}).addTo(map)
        .bindPopup(currentValue.name)
        let markerInList = document.querySelector('#' + currentValue.name);
        currentMarker.on('click', (e) => {
          if (this.isMarkerIsYellow == false) {
            e.target.setIcon(yellowIcon);
            map.setView(e.target.getLatLng(), 10);
            markerInList.style.backgroundColor = "#f8ff91";
            this.isMarkerIsYellow = true;
          }
          else {
            e.target.setIcon(greenIcon);
            map.setView(e.target.getLatLng(), 4);
            markerInList.style.backgroundColor = "white";
            this.isMarkerIsYellow = false;
          }
        });
      });
    }
  },
  mounted() {
    const map = L.map('map').setView([50, 70], 3);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    this.loadingMarkersOnTheMap(map);
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
