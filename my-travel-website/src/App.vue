<template>
 <div id="app">
  <h1>Travel Distance Calculator</h1>
    <DistanceCalculator />
      </div>
</template>

<script>
import DistanceCalculator from './components/DistanceCalculator.vue';

export default {
  name: 'App',
  components: {
       DistanceCalculator
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
