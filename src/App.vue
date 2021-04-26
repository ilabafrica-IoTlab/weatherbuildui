<template>
  
  <HelloWorld msg="WEATHER BUILD"/>

<div id="app">
    <HelloWorld
        ref="map"
        apiKey="AIzaSyBaKeH0sIEWmRiiOlZZi-Kjg5AJbOSIDWQ"
        latitude="37"
        longitude="121"
        zoom="10"
        />
</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted(){
      let map = this.$refs.map;
      map.dropMarker({Latitude: 37, Longitude: -121});
  }
}
</script>

<style 
    body{
      margin:0;
    }
</style>


