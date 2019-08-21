<template>
  <div id="app">
    <Assignment />
  </div>
</template>

<script>
import Assignment from './components/Assignment.vue'

export default {
  name: 'app',
  components: {
    Assignment
  }
}
</script>

<style lang="scss">
    @import "~sanitize.css";

    html {
        font-size: 0.625rem;
    }

    body {
        font-size: 1.6rem;
        line-height: 1.625;
        font-family: Helvetica, Arial, sans-serif;
        -webkit-text-size-adjust: 100%;
        -webkit-font-smoothing: antialiased;
    }
</style>
