<template>
  <div>
    <HelloWorld msg="Hey party on!" otherMSg=" Let the party begun!!"/>
  </div>
</template>

<script setup>
  import HelloWorld from "./components/HelloWorld.vue"
  console.log("Hello World:", HelloWorld);
</script>

<style scoped>

</style>
