<template lang="html">

  <button type="button" name="button" class="btn" v-on:click="$emit('clicked-me', letter)"> {{ letter }} </button>

</template>

<script>
export default {
  props: {
    letter: {
      type : String,
      required : true
    }
  }
}
</script>

<style lang="scss">

.btn {
  margin: 1rem;
  background: rgba(0, 0, 0, .2);
  color: #EEE;
  font-size: 2rem;
  padding: 1rem;
  border-radius: 5px;
  box-sizing: border-box;
  text-transform: uppercase;
  height: 75px;
  width: 75px;
  display: block;
}


</style>
