<template>
  <div id="app">
    <h1 class="heading--1">JS30 - Day 1: Drum Kit</h1>
    <div class="button__container">
        <BaseButton v-for="button in buttons" :letter="button.key" :id="button.key" v-on:clicked-me="playSound" />
    </div>
  </div>
</template>

<script>
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
      ],
      nodeList : []
    }
  },
  methods : {
    playSound: function(key){
    let playMe = this.buttons.filter(button => button.key == key)
    if(playMe.length > 0){
      playMe[0].audio.currentTime = 0;
      playMe[0].audio.play();
      }
    },
    simulatePress(key){
      for(let el of this.nodeList){
        if(el.id == key){
          el.click()
        }
      }
    }
  },
  mounted : function(){
    this.$nextTick(function () {
      // Add Event listeners
      window.addEventListener("keypress", function(e) {
      let key = String.fromCharCode(e.keyCode).toLowerCase()
      this.playSound(key)
      this.simulatePress(key)
    }.bind(this));
    // Add audio elements to the buttons JS only
    this.buttons.forEach(button => button.audio = new Audio(button.sound));
    // Get all buttons from DOM so we can simulate presses
    this.nodeList = document.querySelectorAll('button')

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

h1 {
  background: rgba(0, 0, 0, 0.15);
  display: inline-block;
  padding: 1rem;
  border-radius: 5px;
  color: rgb(167,184,191);
  text-shadow: -5px 5px 3px rgba(0, 0, 0, 0.25);
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

#app {
  max-width: 800px;
  margin: auto;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
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
