<template>
  <AnalyseThis2 />
  <MenuMain />
</template>

<script>
import MenuMain from "@/components/MenuMain.vue";
import AnalyseThis2 from './components/AnalyseThis2.vue';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    MenuMain
    ,AnalyseThis2
}
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
