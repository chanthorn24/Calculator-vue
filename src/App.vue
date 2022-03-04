<template>
  <div id="app">
    <HelloWorld msg="Welcome to the best calculator in the world!" />
    <cal-culator />
  </div>
</template>

<script>
import CalCulator from "./components/AppCalculator.vue";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    CalCulator,
  },
  metaInfo: {
    // if no subcomponents specify a metaInfo.title, this title will be used
    title: "Default Title",
    // all titles will be injected into this template
    titleTemplate: "%s | My Awesome Webapp",
  },
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
