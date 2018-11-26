<template>
  <div id="app">
    <SearchComponent :cities="cities" />
  </div>
</template>

<script>

import SearchComponent from './components/SearchComponent.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    SearchComponent
  },
  data : function(){
    return{
      cities : [],
      endpoint : 'https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json',
    }
  },
  mounted() {
  axios.get(this.endpoint)
    .then((response) => {   console.log(response); this.cities.push(...response.data) })
    .catch((error) => console.log(error))
  }
}
</script>

<style lang="scss">

html {
  font-size: 62.5%;
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}

body {
  font-size: 2.6rem;
  margin: 0;
  padding: 0;
}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
