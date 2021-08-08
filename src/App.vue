<template>
  <div class="container">
    <Header />
    <Main />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Main from '@/components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main
  }
}
</script>

<style>
@import url('./assets/css/reset.css');

:root {
  --primary: #44CE92;
  --primaryText: #2C3E50;
  --background: #E5E5E5;

}

.container {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: var(--primaryText);
}
</style>
