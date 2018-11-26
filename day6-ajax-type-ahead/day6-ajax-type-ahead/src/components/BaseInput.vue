<template>
  <div class="hello">
    <input type="text" name="" value="" v-model="text" placeholder="Search for american cities">
  </div>
</template>

<script>
export default {
  name: 'BaseInput',
  props: {
  },
  data : function(){
    return {
      text : ''
    }
  },
  watch : {
    text : function(){
      this.$emit('search-term', this.text);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

input {
  box-sizing: border-box;
  height: 4.5rem;
  width: 100%;
  padding-left: 2rem;
  font-size: 1.5rem;
  font-weight: 200;
  border-radius: 3px;
  border: 4px solid steelblue;
  background-color: rgba(100, 100, 100, .23);
}

input:focus {
  outline: none;
}

</style>
