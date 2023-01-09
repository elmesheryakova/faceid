<template>
  <div id="app">
    <Auth />
  </div>
</template>

<script>
import Auth from './components/Auth.vue'

export default {
  name: 'App',
  components: {
    Auth
  }
}
</script>

<style>
body {
  display:flex;
  justify-content:center;
  align-items:center;
  height:100vh
}
</style>
