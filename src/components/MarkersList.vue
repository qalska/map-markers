<template>
  <div class="markers">
    <h2 class="markers__h2">Объекты</h2>
    <input class="markers__search"
           type="text"
           placeholder="Поиск"
           v-model="search">
    <ul class="markers__list">
      <li class="markers__item" 
          v-for="marker in markersByName" 
          :key="marker.id">{{ marker.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
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
      ]
    }
  },
  computed: {
    markersByName() {
      return this.markers.filter(item => item.name.indexOf(this.search) !== -1)
    },
  },
}
</script>

<style lang="scss" scoped>
  li{
    list-style-type: none;
  }
  ul{
    margin-left: 0;
    padding-left: 0;
  }
  .markers{
    float: right;
    font-family: 'Roboto', sans-serif;
    border-radius: 8px;
    width: 20%;
    &__h2{
      font-size: 24px;
      padding-left: 20px;
    }
    &__search{
      border: none;
      outline: none;
      outline-offset: 0;
      width: 100%;
      background-color: #F2F2F2;
      font-size: 16px;
      padding: 10px 0;
      margin-left: 2%;
      &::placeholder{
        font-family: 'Roboto', sans-serif;
        color: black;
        padding: 20px;
      }
    }
    &__list{
      padding: 20px;
    }
    &__item{
      position: relative;
      padding: 5px 0 5px 20px;
      border-bottom: 1px #EDEDED solid;
      &::before{
        content: '';
        background: url('../assets/car.svg') 0 0 no-repeat;
        width: 100%;
        height: 100%;
        position: absolute;
        top: 9px;
        left: 0;
      }
    }
  }
</style>
