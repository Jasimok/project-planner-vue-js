<template>
    <nav-componet></nav-componet>
  <router-view/>
</template>

<script>
import NavComponet from "./components/NavComponet.vue";
export default {
    components: {
        NavComponet
    },
}
</script>
<style>
body {
    background-color: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0px auto;
  color: #555;
}

</style>
