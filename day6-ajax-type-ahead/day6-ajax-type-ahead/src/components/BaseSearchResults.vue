<template>
  <div class="">
    <ul>
      <li v-for="city in cities" :key="city.rank">
        <div class="li-content">
            <span>{{city.rank}} - {{ city.city}}</span><span> {{city.state}}</span> <span>{{city.population}}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'BaseSearchResults',
  props: {
    cities : {
      type: Array
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  ul {
    list-style: none;
    padding-left: 0;
    margin: 0;
    width: 95%;
    margin: auto;
    margin-bottom: 4rem;
  }

  li {
    padding: 1rem 2rem;
    color: ivory;

    &:nth-child(odd){
      transform: skewX(8deg);
      background-color: steelblue;
      & > .li-content {
        transform: skewX(-8deg);
      }
    }
    &:nth-child(even){
      transform: skewX(-8deg);
      background-color: tomato;
      & > .li-content {
        transform: skewX(8deg);
      }
    }
  }

  .li-content {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
</style>
