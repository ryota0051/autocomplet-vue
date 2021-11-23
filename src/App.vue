<template>
  <div id="app">
    <AutoComplete v-model="text" />
  </div>
</template>

<script>
import AutoComplete from "./components/AutoComplete.vue"

export default {
  name: "App",
  components: {
    AutoComplete,
  },
  data() {
    return {
      text: "",
    }
  },
}
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
