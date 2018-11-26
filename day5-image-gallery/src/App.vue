<template>
  <div id="app">
    <div v-for="panel in panels" :key="panel.id" class="panel">
      <Transition name="fade" appear>
        <ImagePanel :src="panel.url" :text="panel.text" :panelId="panel.id" v-show="panel.image.loaded"/>
      </Transition>
    </div>
  </div>
</template>

<script>
import ImagePanel from './components/ImagePanel.vue';

export default {
  name: 'app',
  components: {
    ImagePanel,
  },
  data : function(){
    return {
      panels : [
        {id: 1, text: ['Hey','Let\'s','Dance'], url : 'https://source.unsplash.com/gYl-UtwNg_I/1500x1500', image : {loaded : false, DOM : ''}},
        {id: 2, text: ['Give','Take','Receive'], url : 'https://source.unsplash.com/rFKUFzjPYiQ/1500x1500', image : {loaded : false, DOM : ''}},
        {id: 3, text: ['Experience','It','Today'], url : 'https://images.unsplash.com/photo-1465188162913-8fb5709d6d57?ixlib=rb-0.3.5&q=80&fm=jpg&crop=faces&cs=tinysrgb&w=1500&h=1500&fit=crop&s=967e8a713a4e395260793fc8c802901d', image : {loaded : false, DOM : ''}},
        {id: 4, text: ['Give','All','You Can'], url : 'https://source.unsplash.com/ITjiVXcwVng/1500x1500', image : {loaded : false, DOM : ''}},
        {id: 5, text: ['Life','In','Motion'], url : 'https://source.unsplash.com/3MNzGlQM7qs/1500x1500', image : {loaded : false, DOM : ''}}
      ]
    }
  },
  beforeMount : function(){
    this.panels.forEach(function(panel){
       panel.image.DOM = new Image(panel.url)
    )
  },
  mounted : function(){
    let parent = document.querySelector('#app');
    parent.addEventListener('click', function(e){
      let el = e.path.filter(el => el.className == 'panel' )
      let panels = [...document.querySelectorAll('.panel')];
      panels.forEach(function(panel){
        panel.classList.remove('active')
      })
      if(el.length > 0){
        el[0].classList.add('active')
      }
    })
  }
};
</script>

<style lang="scss">

html {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
}

body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: row;
  width: 100vw;
  height: 100%;
  overflow-y: hidden;
}

.active {
  flex-grow: 1 !important;
  flex-basis: 60vw !important;
}

.panel {
  width: 100%;
  height: 100%;
  flex-grow: 2;
  flex-basis: 20vw;
  transition: all .15s ease-out;
}

.panel.active > .panel__content p {
  font-size: 4em;
}
.panel.active > .panel__content p:first-child{
  transform: translateY(0);
}
.panel.active > .panel__content p:last-child {
  transform: translateY(0);
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
