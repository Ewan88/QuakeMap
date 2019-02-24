<template>
  <div id="app">

    <div id="ui">
      <div id="form">
        <label for="from">from:</label>
        <input id="from" type="date" v-model="from"/>

        <label for="to">to:</label>
        <input id="to" type="date" v-model="to"/>

        <label for="mag">mag:</label>
        <input id="mag" type="number" v-model="mag" max="10" min="0"/>

        <button v-on:click="getEvents">
          search
        </button>
      </div>

      <div id="drop-down">
        <event-list :events="events"/>
      </div>

      <div id="detail" v-if="selectedEvent">
        <event-detail :event="selectedEvent"/>
      </div>
    </div>

  </div>
</template>

<script>
import EventList from './components/EventList.vue';
import EventDetail from './components/EventDetail.vue';
import { eventBus } from './main.js';

export default {
  name: 'app',
  data(){
    return {
      from: '2019-02-12',
      to: '2019-02-22',
      mag: '5',
      events: {},
      selectedEvent: null,
    };
  },
  components: {
    "event-list": EventList,
    "event-detail": EventDetail,
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

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
