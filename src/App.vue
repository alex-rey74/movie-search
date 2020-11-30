<template>
  <div id="app">
    <Search/>
  </div>
</template>

<script>
/* eslint-disable no-console */
import Search from '@/components/Search'

export default {
  name: 'app',
  components:{
    Search,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
