<template lang="html">
  <select v-model="selectedEvent" v-on:change="handleSelect">
    <option v-for="(event, index) in events.features" :key="index" :value="event">
      {{event.properties.title}}
    </option>
  </select>
</template>

<script>
import { eventBus } from '../main.js';
export default {
  data(){
    return {
      selectedEvent: null,
    }
  },
  name: 'event-list',
  props: ['events'],
  methods: {
    handleSelect(){
      eventBus.$emit('selected-event', this.selectedEvent);
    }
  }
}
</script>
