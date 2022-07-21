<template>
  <div>
        <router-view></router-view>
        <router-view name="Home"></router-view>
  </div>
</template>

<script>
// import BeiJing from "./components/BeiJing.vue"
// import LogIn from "./components/LogIn.vue"
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
// import HomePage from "./views/HomePage.vue";
// import TopPop from './components/TopPop.vue'
export default {
  components: {
    // BeiJing,
    // LogIn,
    // TopPop,
    // HomePage,
  },
};
</script>

<style>
</style>
