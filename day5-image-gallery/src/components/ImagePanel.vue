<template>
  <div :ref="panelId" class="panel__content" v-cloak>
    <p v-for="word in text">
      {{word}}
    </p>
  </div>
</template>

<script>
export default {
  name: 'ImagePanel',
  props: {
    src: String,
    text: Array,
    panelId: Number
  },
  data : function() {
    return {
      image : ''
    }
  },
  beforeMount : function() {
    this.image = new Image();
    this.image.src = this.src
  }
  ,
  mounted : function(){
    this.$refs[this.panelId].style.backgroundImage = `url(${this.image.src})`
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

[v-cloak] {
  display: none;
  opacity: 0;
}

.panel__content{
  opacity: 1;
    margin: 0;
    width: 100%;
    height: 100%;
    transition: all 0.5s;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;

  & p {
    text-transform: uppercase;
    font-family: 'Amatic SC', cursive;
    text-shadow: 0 0 4px rgba(0, 0, 0, 0.72), 0 0 14px rgba(0, 0, 0, 0.45);
    font-size: 2em;
    user-select: none;
    transition: all .3s;
  }

  & p:first-child{
    transform: translateY(-30vh);
  }
  & p:last-child {
    transform: translateY(30vh);
  }
}
</style>
