<template>
  <div class="hello">
    <h1 class="text-3xl text-pink-500 font-bold">{{ msg }}</h1>
    
    <div class="topnav">
 
  <input type="text" placeholder="Search..">
</div>
   <div ref="map" style="width: 100vw; height: 100vh"></div>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      platform:{},
      map:{},
      geocodingService:{}
    
    }
  },
  props: {
    apikey:String,
    latitude:String,
    longitude:String,
    zoom:String,
    msg: String
  },
  created(){
    this.platform = new H.service.platform({
      "apikey": this.apiKey
    });
    this.geocodingService = this.platform.getGeocodingService();
  },
  mounted(){
    this.map = new H.Map(
      this.$refs.map,
      this.platform.createDefaultLayers().vector.normal.map,
      {
        zoom: this.zoom,
        center:{lat: this.latitude, lng:this.longitude}
      }
    );
  },
  methods:{
    dropMarker(query){
        this.geocodingService.geocode({searchText: query}, data =>{
         if(data.Response.View.length > 0) {
           if(data.Response.View[0].Result.length > 0){
             let position = data.Response.View[0].Result[0].Location.DisplayPosition;
           }
         }
        },error =>{
          console.error(error);
        });

     /* let marker = new H.map.Marker({ lat: position.Latitude, lng: position.Longitude});
      this.map.addObject(marker);*/
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
