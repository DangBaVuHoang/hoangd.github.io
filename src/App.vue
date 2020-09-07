<template>
  <div id="app">
    <ToDo></ToDo>
    <options></options>
  </div>
</template>
<script>

import ToDo from "./components/todo.vue"
import options from "./components/option.vue"

export default {
  components: {
    ToDo,
    options
  }
}
</script>
<style>
  #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>