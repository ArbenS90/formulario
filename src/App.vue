<template>


<link href="/dist/output.css" rel="stylesheet">

  <MenuFormulario/>
</template>

<script>

import MenuFormulario from './components/MenuFormulario.vue';


export default {
  name: 'App',
  components: {
    MenuFormulario

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
  margin-bottom: 60px;
}
</style>
