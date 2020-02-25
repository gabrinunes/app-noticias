<template>
  <div id="app">
    <app-noticias/>
  </div>
</template>

<script>
import AppNoticias from './components/Noticias'
export default {
     components:{AppNoticias}
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
