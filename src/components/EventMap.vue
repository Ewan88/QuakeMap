<template lang="html">
  <div id="event-map"></div>
</template>

<script>
export default {
  name: 'event-map',
  props: ['events'],
  data(){
    return {
      mapObject: null,
      eventsObject: null,
    };
  },
  mounted(){
    this.initMap();
    this.handleContextLoss();
  },
  methods: {
    initMap(){
      var mapboxgl = require('mapbox-gl/dist/mapbox-gl.js');

      mapboxgl.accessToken = 'pk.eyJ1Ijoicm9kZ2VyLXRoZS1zaHJ1YmJlciIsImEiOiJjanNqZ3gxNnoyYXFyNDN0YnV2dGVjeTl1In0.7YUhBJNDpqGmjW8iLzpgaQ';

      this.mapObject = new mapboxgl.Map({
        container: 'event-map',
        style: 'mapbox://styles/mapbox/satellite-v9',
      });

      this.eventsObject = this.events;

      this.mapObject.on('load', function(){

        this.mapObject.addLayer({
          "id": "points",
          "type": "symbol",
          "source": {
            "type": "geojson",
            "data": this.eventsObject,
          },
          "layout": {

          }
        });
      });
    },
    handleContextLoss(){
      var canvas = document.getElementById("event-map");
      canvas.addEventListener("webglcontextlost", function(event) {
        event.preventDefault();
      }, false);
    },
  },
}
</script>
