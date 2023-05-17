<template>
  <div id="app">
    <AppHeader/>
    <TheBoard />
    <AppFooter/>
  </div>
</template>

<script>
import TheBoard from './components/TheBoard.vue';
import AppHeader from './components/AppHeader.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  components: {
    TheBoard,
    AppHeader,
    AppFooter
  },
};
</script>

<style>
#app {
  font-family: 'Arial', sans-serif;
}
</style>
