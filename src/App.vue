<template>
  <div id="app">
    <ClockCountdown msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import ClockCountdown from './components/ClockCountdown.vue'

export default {
  name: 'App',
  components: {
    ClockCountdown
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
* {
  margin: 0;
  padding: 0;
  background-color: #ccc;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 120px;
  
}
</style>
