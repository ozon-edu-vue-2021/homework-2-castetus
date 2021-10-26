<template>
  <div id="app">
    <tree></tree>
    <navigation></navigation>
  </div>
</template>

<script>
import Tree from './components/Tree.vue';
import Navigation from './components/Navigation.vue';

export default {
  name: 'App',
  components: {
    Tree,
    Navigation,
  }
}
</script>

<style>
*{
  box-sizing: border-box;
}
li{
  list-style-type: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: space-between;
}
</style>
