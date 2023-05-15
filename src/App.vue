<template>
  <!--<img alt="Vue logo" src="./assets/logo.png">-->
  <v-wrapper></v-wrapper>
</template>

<script>
import vWrapper from './components/v-wrapper.vue';
export default {
  name: 'App',
  components: {
    vWrapper
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
  margin: 0;
}
body{
  margin:0;
  padding: 0;
}
</style>
