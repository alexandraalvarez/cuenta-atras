<template>
  <div id="app">
    {{ message }}
  </div>
</template>

<script>
  export default {
    data() {
      return {
        message: 'Hola en vue',
      };
    }
  }
</script>

<style scoped>
  #app {
    font-size: 25px;
    font-family: "Calibri", sans-serif;
    color: darkblue;
    background: lightblue;
  }
</style>
