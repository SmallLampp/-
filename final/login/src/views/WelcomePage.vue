<template>
  <div class="hah" style="position:absolute;left:0;right:0;top:0;bottom:0;overflow:hidden;">
    <!-- <h1>欢迎登录 亲爱的 {{this.$store.state.currDbSource.account}}</h1> -->
    <DaohangView></DaohangView>>
  </div>
</template>
<script>
  import DaohangView from "../components/DaohangView.vue"
  export default{
    comments: {
        DaohangView,
    },
    components: { DaohangView }
}
</script>

<style>
</style>