<template>
  
  <homepage msg="Welcome to Your Vue.js App"/>

  <!-- <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
  </div> -->
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

// export default {
//   name: 'App',
//   components: {
//     HelloWorld
//   }
// }

import homepage from './components/homepage.vue'

export default {
  name: 'App',
  components: {
    homepage
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
