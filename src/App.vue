<!-- App.vue -->
<template>
  <div id="app">
    <div class="header">
      <!--<img src="logo.png" alt="Logo" />-->
    </div>
    <WeatherUi />
  </div>
</template>

<script>
import WeatherUi from './components/Weather.vue'


export default {
  name: 'App',
  components: {
    WeatherUi
  }
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
}

.header {
  /* 页眉的样式 */
}
</style>
