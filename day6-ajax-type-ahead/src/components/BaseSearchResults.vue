<template>
  <div class="results">
    <ul>
      <li v-for="city in cities" :key="city.rank">
        <div class="li-content">
            <span>{{city.city}} - {{city.state}}</span> <span class="li-content--pop">{{city.population}}</span>
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
  },
  computed : {},
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
    color: rgba(0, 0, 0, .85);
    background-color: #F0F0F0;
    margin-bottom: 1px;

    &:nth-child(odd){
      transform: skewX(8deg);
      & > .li-content {
        transform: skewX(-8deg);
      }
    }
    &:nth-child(even){
      transform: skewX(-8deg);
      & > .li-content {
        transform: skewX(8deg);
      }
    }
  }

  .li-content {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: center;

    & > span {
      display: inline-block;
    }
  }


  .li-content--pop {
    display: inline-block;
    margin-left: auto;
  }
</style>
