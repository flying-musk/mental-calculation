<template>
  <div id="app">
    <MentalCalculation />
  </div>
</template>

<script>
import MentalCalculation from './components/MentalCalculation.vue';
export default {
  name: 'App',
  components: { MentalCalculation },
};
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
