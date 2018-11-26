<template>
  <div class="search-box">
    <BaseInput v-on:search-term="search"/>
    <transition name="list">
      <BaseSearchResults v-if="show" :cities="filteredSearch"/>
    </transition>
  </div>
</template>

<script>
import BaseInput from './BaseInput.vue';
import BaseSearchResults from './BaseSearchResults.vue';

export default {
  name: 'SearchComponent',
  components: {
    BaseSearchResults,
    BaseInput
  },
  data : function(){
    return {
      filteredSearch : [],
      show : false,
    }
  },
  props: {
    cities : {
      type: Array
    }
  },
  methods : {
    search : function(term){
      let rgx = new RegExp(term, 'giu')
      term.length > 0 ? this.filteredSearch = this.cities.filter( city =>rgx.test(city.city)) : this.filteredSearch = []
    },
  },
  watch : {
    filteredSearch : function(el){
      el.length > 0 ? this.show = true : this.show = false
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.search-box {
  width: 60vw;
  margin: auto;
}

.list-enter-active, .list-leave-active {
  transition: all .25s;
  height: 100%;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0.4;
  height: 0;
}

</style>
