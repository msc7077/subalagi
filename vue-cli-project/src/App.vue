<template>
  <div id="app">
    <memo-app/>
  </div>
</template>

<script>
import MemoApp from './components/MemoApp.vue';

export default {
  name: 'App',
  components: {
    MemoApp,
  }
}
</script>

<style>

@import "./styles/reset.css";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
