<template>
  <div id="app">
    <Test />
    <TwoSwiper :previewCount="4" />
  </div>
</template>

<script>
//import HelloWorldVue from "./components/HelloWorld.vue";
// import MenuSwiper from "./components/MenuSwiper.vue";
import Test from "./components/Test.vue";
import TwoSwiper from "./components/TwoSwiper.vue";
import Test2 from "./components/Test2.vue";
export default {
  name: "App",
  components: {
    // HelloWorld: HelloWorldVue,
    // MenuSwiper: MenuSwiper,
    Test: Test,
    TwoSwiper: Test2,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #222;
  margin-top: 60px;
}
</style>
