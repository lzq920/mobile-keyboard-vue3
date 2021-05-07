<template>
  <p @click="show = !show">{{ inputValue }}</p>
  <keyboard v-model="inputValue" type="card" v-model:show="show"></keyboard>
</template>
<script setup>
import keyboard from './components/keyboard.vue'
import {ref} from "vue"
const inputValue = ref('123')
const show = ref(true)
</script>
<style>
html, body {
  margin: 0;
  padding: 0;
}
</style>
