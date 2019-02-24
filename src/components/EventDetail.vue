<template lang="html">
  <div>
    <p>{{event.properties.place}}</p>
    <p>{{event.properties.mag}} mb</p>
    <p>{{event.geometry.coordinates[2]}} km</p>
    <p>
      {{event.geometry.coordinates[0]}}
      {{event.geometry.coordinates[1]}}
    </p>
  </div>
</template>

<script>
export default {
  name: "event-detail",
  props: ["event"]
}
</script>

<style lang="css" scoped>

</style>
