<template>
  <div id="app">
    <UserModal />
  </div>
</template>

<script>
import UserModal from './components/UserModal.vue';

export default {
  name: 'App',
  components: {
    UserModal
  }
};
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
