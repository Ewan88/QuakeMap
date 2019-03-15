<template lang="html">
  <MglMap
    :accessToken="accessToken"
    :mapStyle="mapStyle"
    id="event-map"
  >
    <MglMarker :coordinates="coordinates" color="blue" />
  </MglMap>
</template>

<script>
import Mapbox from "mapbox-gl";
import { MglMap, MglMarker } from "vue-mapbox";

export default {
  name: 'event-map',
  props: ['events'],
  components: {
    MglMap,
    MglMarker
  },
  data() {
    return {
      accessToken: 'pk.eyJ1Ijoicm9kZ2VyLXRoZS1zaHJ1YmJlciIsImEiOiJjanNqZ3gxNnoyYXFyNDN0YnV2dGVjeTl1In0.7YUhBJNDpqGmjW8iLzpgaQ',
      mapStyle: 'mapbox://styles/mapbox/satellite-streets-v11',
      coordinates: [
        this.events.features[0].geometry.coordinates[0],
        this.events.features[0].geometry.coordinates[1] 
      ]
    };
  },
  created() {
    this.mapbox = Mapbox;
    // console.log(this.mapbox);
    // this.MglMap.addSource('event-map', {
    //   type: 'geojson',
    //   data: this.events,
    // });
  },
  methods: {

  },
};


  // name: 'event-map',
  // props: ['events'],
  // data(){
  //   return {
  //     mapObject: null,
  //     // eventsObject: null
  //   };
  // },
  // mounted(){
  //   this.initMap();
  //   // this.initLayers();
  //   this.handleContextLoss();
  // },
  // methods: {
  //   initMap(){
  //     var mapboxgl = require('mapbox-gl/dist/mapbox-gl.js');
  //     mapboxgl.accessToken = 'pk.eyJ1Ijoicm9kZ2VyLXRoZS1zaHJ1YmJlciIsImEiOiJjanNqZ3gxNnoyYXFyNDN0YnV2dGVjeTl1In0.7YUhBJNDpqGmjW8iLzpgaQ';
  //     this.mapObject = new mapboxgl.Map({
  //       container: 'event-map',
  //       style: 'mapbox://styles/mapbox/satellite-streets-v11',
  //     });
  //   },
  //   handleContextLoss(){
  //     var canvas = document.getElementById("event-map");
  //     canvas.addEventListener("webglcontextlost", function(event) {
  //       event.preventDefault();
  //     }, false);
  //   },
  // },
// }
</script>
