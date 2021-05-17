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
export default {
  components: {
    MarkersList
  },
  data() {
    return {
      markers: [
        {
          "id": 1,
          "latitude": 50.760918,
          "longitude": 4.110170,
          "name": "ВАЗ"
        },
        {
          "id": 2,
          "latitude": 47.492647,
          "longitude": 19.051399,
          "name": "ГАЗель"
        },
        {
          "id": 3,
          "latitude": 41.902689,
          "longitude": 12.496176,
          "name": "Lexus"
        },
        {
          "id": 4,
          "latitude": 43.779787,
          "longitude": 11.265817,
          "name": "Volkswagen"
        },
        {
          "id": 5,
          "latitude": 52.373057,
          "longitude": 4.892557,
          "name": "Lada"
        },
        {
          "id": 6,
          "latitude": -22.903150,
          "longitude": -43.189903,
          "name": "Kia"
        },
        {
          "id": 7,
          "latitude": 38.716174,
          "longitude": -9.141589,
          "name": "Bentli"
        },
        {
          "id": 8,
          "latitude": 50.080293,
          "longitude": 14.428983,
          "name": "Porche"
        },
        {
          "id": 9,
          "latitude": 48.856663,
          "longitude": 2.351556,
          "name": "BMW"
        },
        {
          "id": 10,
          "latitude": 45.438095,
          "longitude": 12.319029,
          "name": "Honda"
        }
      ],
    }
  },
  methods: {
  },
  mounted() {
    const map = L.map('map').setView([50, 70], 3);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

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
    
    this.markers.forEach( (currentValue) => {
        let currentMarker = L.marker([currentValue.latitude, currentValue.longitude]).addTo(map)
        .bindPopup(currentValue.name)
        currentMarker.on('click', (e) => {
          e.target.setIcon(greenIcon);
          map.setView(e.target.getLatLng(), 10);
        }); 
      });
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
