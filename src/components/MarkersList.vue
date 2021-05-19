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
          :key="marker.id"
          :id="marker.name">
          <img class="markers__img" 
               src="@/assets/car.svg" 
               alt="car">
          {{ marker.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    markers: {
      type: Array,
      required: false,
      default: [],
    },
  },
  data() {
    return {
      search: '',
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
      margin-left: 0;
      padding-left: 0;
      padding: 20px;
    }
    &__item{
      list-style-type: none;
      position: relative;
      padding: 5px 0 5px 0px;
      border-bottom: 1px #EDEDED solid;
    }
  }
</style>
