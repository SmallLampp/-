<template>
    <div>
        <div>
            <TopPop></TopPop>
        </div>
     
        <div>
            <BeiJing>
            <LogIn></LogIn>
        </BeiJing>
        <LogIn></LogIn>
        </div>
        <div>
            <badgeView></badgeView>
        </div>
    </div>
</template>

<script>
import BeiJing from "../components/BeiJing.vue"
import LogIn from "../components/LogIn.vue"
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import TopPop from '../components/TopPop.vue'
import badgeView from "../components/BadgeView.vue"
export default{
    components:{
        BeiJing,
        LogIn,
        TopPop,
        badgeView,
    }
}
</script>

<style>

</style>
