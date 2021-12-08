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
*{
 background-color:rgb(255, 233, 198);
}
#app {
  font-family: Arial, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
