<template>

  <div style="height: 600px; wight:90%;">

    
    <l-map
      style="height: 80%; width: 100%"
      :zoom="zoom"
      :center="center"
      :minZoom=2
      
      @update:zoom="zoomUpdated"
      @update:center="centerUpdated"
      @update:bounds="boundsUpdated"  
    >

    

    <l-marker

    v-for="(da,index) in dati"
    :key="index"
    :lat-lng="latLng(da.latitude,da.longitude)"
    >
    <l-popup  
    >Latitudine = {{da.latitude}} <br> Longitudine = {{da.longitude}} <br> Data = {{da.date}}
    </l-popup></l-marker>
    
      <l-tile-layer :url="url"></l-tile-layer>
    </l-map>
  </div>
</template>

<script>
import L from "leaflet"; 
import {LMap, LTileLayer, LMarker, LPopup} from 'vue2-leaflet';
export default {
    name:"FireMap",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      zoom: 2,
      center: [37.5093, 13.0889],
      bounds: null,
        
          
       };
  },
  props:{
    dati:Array
  },
   
  methods: {
    zoomUpdated (zoom) {
      this.zoom = zoom;
    },
    centerUpdated (center) {
      this.center = center;
    },
    boundsUpdated (bounds) {
      this.bounds = bounds;
    },
    latLng: function(lat, lng){
        return L.latLng(lat,lng);
    }
  },
  
}
</script>

<style scoped>

</style>