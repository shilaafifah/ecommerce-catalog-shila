<template>
  <div id="app">
    
    <ProductDisplay/>
  </div>
</template>

<script>
import ProductDisplay from './components/ProductDisplay'

export default {
  name: 'App',
  components: {
    ProductDisplay
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
