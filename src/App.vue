<template>
  <div id="app">
    <vue-drag-form />
  </div>
</template>

<script>
import VueDragForm from './components/VueDragForm'

export default {
  name: 'App',
  
  components: {
    VueDragForm
  }
}
</script>

<style lang="less">
html, body {
  margin: 0;
  padding: 0
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
