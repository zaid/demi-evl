<template>
  <div id="app">
    <Header />
    <Dashboard />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Dashboard from './components/Dashboard.vue'

export default {
  name: 'app',
  components: {
    Header,
    Dashboard
  }
}
</script>

<style>
#app {
}
</style>
