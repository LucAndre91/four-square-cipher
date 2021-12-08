<template>
  <div>
    <Cipher />
  </div>
</template>

<script>
import Cipher from './components/Cipher.vue'

export default {
  name: 'App',
  components: {
    Cipher
  }
}
</script>

<style>
#app {
  font-family: Arial, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
