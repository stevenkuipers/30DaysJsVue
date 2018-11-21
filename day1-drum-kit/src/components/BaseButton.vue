<template lang="html">
  <button :ref="letter" type="button" name="button" class="btn" v-on:click="$emit('clicked-me', letter); addActive($refs[letter])"> {{ letter }} </button>
</template>

<script>
export default {
  props: {
    letter: {
      type : String,
      required : true
    }
  },
  mounted : function(){
    let el = this.$refs[this.letter];
    el.addEventListener("transitionend", function(event) {
      el.classList.remove('active')
    }.bind(this));
  },
  methods : {
    addActive : function(el){
      el.classList.add('active')
    }
  }
}
</script>

<style lang="scss" scoped>
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
  transform: scale(1);
  transition: all .075s;
  box-shadow: -2px 4px 8px -5px rgba(255,175,189,0.2);
}

.btn:active, .btn:focus {
  outline: none;
}

.active {
  box-shadow: -2px 0px 68px 9px rgba(255,175,189,0.2);
  transform: scale(1.8);
}
</style>
