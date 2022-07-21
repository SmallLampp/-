<template >
    <div>
        <transition name="fade" @after-enter='Enter' @after-leave='Leave' >
            <img src="@/assets/xx.jpg" alt="" class="xh" v-show="show">
        </transition>

    </div>
</template>

<script>
    export default{
        created(){
        },
        mounted(){
            this.show = !this.show
        },
        data(){  
            return {
                show:false,
                flag:true,
                show2:false,
            }
        },
        methods:{
            Enter(){
                this.show=!this.show;
            },
            Leave(){
                this.show=!this.show;
            }
        }
       
    }
</script>

<style lang="css" scoped>
.xh{
    position: absolute;
    right: 23%;
    top: 23%;
    width: 60px;
    height: 60px;
}
.fade-enter
{
    opacity: 0;
}
.fade-leave-to{
    opacity: 0;
}
.fade-enter-to,.fade-leave{
    opacity: 1;
}
.fade-enter-active,.fade-leave-active{
    transition: all 2s;
}

</style>

