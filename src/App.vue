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
 background-color:rgb(168, 192, 228);
}
#app {
  font-family: Arial, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}
</style>
