<template>
  <div id="app">
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
body{
  background-image: url('https://picsum.photos/1920/1080');
  background-repeat: no-repeat;
}
</style>
