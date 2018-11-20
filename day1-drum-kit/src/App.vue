<template>
  <div id="app">
    <h1>Hello All</h1>
    <div class="button__container">
        <BaseButton v-for="button in buttons" :letter="button.key" v-on:clicked-me="playSound" />
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  data : function(){
    return {
      buttons : [
        { key :'q' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/808-kick-vh.mp3'} ,
        { key :'w' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/808-kick-vm.mp3'} ,
        { key :'e' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/808-kick-vl.mp3'} ,
        { key :'a' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/808-hihat-vh.mp3'},
        { key :'s' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/808-hihat-vm.mp3'},
        { key :'d' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/808-hihat-vl.mp3'},
        { key :'z' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/909-clap-vh.mp3'} ,
        { key :'x' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/909-clap-vm.mp3'} ,
        { key :'c' , sound : 'https://s3-us-west-2.amazonaws.com/s.cdpn.io/969699/909-clap-vl.mp3'}
      ]
    }
  },
  methods : {
    playSound: function(key){
    let playMe = this.buttons.filter(button => button.key == key)
    if(playMe.length > 0){
      playMe[0].audio.currentTime = 0;
      playMe[0].audio.play();
      }
    }
  },
  mounted : function(){
    this.$nextTick(function () {
      // Add Event listeners
      window.addEventListener("keypress", function(e) {
      let key = String.fromCharCode(e.keyCode).toLowerCase()
      this.playSound(key)
    }.bind(this));
    // Add audio elements to the buttons JS only
    this.buttons.forEach(button => button.audio = new Audio(button.sound));
  })
  }
};
</script>

<style lang="scss">

html {
  min-height: 100%;
  min-width: 100%;
  box-sizing: border-box;
}

body {
  box-sizing: inherit;
  min-height: 100%;
  background: #ffafbd; /* fallback for old browsers */
  background-image: -webkit-linear-gradient(to top, rgba(255,175,189, .3), rgba(255,195,159, .3)), url(https://source.unsplash.com/nPz8akkUmDI/1600x900);
  background-image: linear-gradient(to top, rgba(255,175,189, .3), rgba(255,195,159, .3)), url(https://source.unsplash.com/nPz8akkUmDI/1600x900);
}

#app {
  max-width: 800px;
  margin: auto;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.button__container {
  padding: 1rem;
  display: grid;
  grid-gap: 2rem;
  grid-template-columns: repeat(3, 1fr);
  justify-items: center;
  align-items: center;

}
</style>
