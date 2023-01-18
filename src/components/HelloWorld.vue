
<template>
    <div>
      <h1>{{ msg }}</h1>

      <h6>{{ otherMSg }}</h6>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from "vue";
    defineProps(["msg", "otherMSg"]);
  </script>
  
  <style scoped></style>
  