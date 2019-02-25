<template>
  <div id="app">
    <event-map v-if="events" :events="events"/>
    <div id="center" class="container">
      <event-list :events="events"/>
      <event-detail v-if="selectedEvent" :event="selectedEvent"/>
    </div>
    <div id="left" class="container">
      <label for="from">from:</label>
      <input class="from" type="date" v-model="from" v-on:input="getEvents">

      <label for="to">to:</label>
      <input class="to" type="date" v-model="to" v-on:input="getEvents"/>

      <label for="mag">mag:</label>
      <input class="mag" type="number" v-model="mag" max="10" min="0" v-on:input="getEvents"/>
    </div>
  </div>
</template>

<script>
import EventList from './components/EventList.vue';
import EventDetail from './components/EventDetail.vue';
import EventMap from './components/EventMap.vue'
import { eventBus } from './main.js';

export default {
  name: 'app',
  data(){
    return {
      from: '2019-02-12',
      to: '2019-02-22',
      mag: '5',
      events: null,
      selectedEvent: null,
    };
  },
  components: {
    "event-list": EventList,
    "event-detail": EventDetail,
    "event-map": EventMap,
  },
  mounted(){
    this.getEvents();
  },
  methods: {
    getEvents(){
      fetch(`https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=${this.from}&endtime=${this.to}&minmagnitude=${this.mag}`)
      .then(res => res.json())
      .then(events => this.events = events)

      eventBus.$on('selected-event', (event) => {
        this.selectedEvent = event;
      });
    },
  }
}
</script>
