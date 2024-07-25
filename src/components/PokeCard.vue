<template>
  <li>
    <h4>
      {{ number }}
    </h4>
    <h2>
      {{ name }}
    </h2>
  </li>
</template>

<script setup>
 import { defineProps } from 'vue';

 defineProps({
    number: {
      type: Number,
      required: true
    },

    name: {
      type: String,
      required: true
    }
 })
</script>

<style scoped>
li {
  display: block;
  width: 80vw;
  margin: 10px;
  padding: 5% 0;
  text-align: center;
  background-color: darkslategrey;
}
</style>