<template>
  <div id="app">
    <Dashboard></Dashboard>
    <router-view />
  </div>
</template>

<script>
import Dashboard from '../src/components/Dashboard'
export default {
  components: {
    "Dashboard":Dashboard
  }
}
</script>

<style lang="scss">
@import '../src/scss/main.scss';
</style>
