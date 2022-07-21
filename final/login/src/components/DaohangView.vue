
<template>
    <div style="height: 100%;">
    <el-container style="height: 100%; border: 1px solid #eee" >
        <el-header style="text-align: right; font-size: 20px">
            <el-button @click="zhankai" :icon="iconType" style="position:absolute;left:0.4%;top:1%;background-color: #B3C0D1 ;border: 1px solid #B3C0D1"></el-button>
            <label for="" style="position:absolute;left: 10%;">学生成绩分析系统</label>
            <el-dropdown>
                <i class="el-icon-user-solid" style="margin-right: 20px"></i>
                <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item>个人空间</el-dropdown-item>
                    <el-dropdown-item>设置</el-dropdown-item>
                    <el-dropdown-item>联系方式</el-dropdown-item>
                    <el-dropdown-item  @click.native="LogOut" >注销</el-dropdown-item>   <!--需要设置native修饰才能使用点击事件 -->
                </el-dropdown-menu>
            </el-dropdown>
            <span class="Helvetica Neue">{{this.$store.state.currDbSource.account}}</span>
        </el-header>
        
        <el-container style="height: 100%;" >
            <el-aside width="" style="background-color: rgb(238, 241, 246)">
                <el-menu style="min-height:auto"   default-active="1-4-1" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" :collapse="isCollapse">
                <el-submenu index="1">
                    <template slot="title">
                    <i class="el-icon-s-data"></i>
                    <span slot="title">分析</span>
                    </template>
                    <el-menu-item-group>
                    <span slot="title">视图</span>
                    <el-menu-item @click="ToCharts" index="1-1">成绩</el-menu-item>
                    </el-menu-item-group>
                </el-submenu>
                <el-menu-item index="3" >
                    <i class="el-icon-document"></i>
                    <span @click="ToDocument" slot="title">文档</span>
                </el-menu-item>
                <el-menu-item index="4">
                    <i class="el-icon-setting"></i>
                    <span slot="title">设置</span>
                </el-menu-item>
                </el-menu>
            </el-aside>
            
            <el-main>
                
                <transition name="fade">
                    <ChartView v-show="flag"></ChartView>
                </transition>
                <DocumentView v-show="!flag"></DocumentView>
            </el-main>
        </el-container>
    </el-container>
    </div>
</template>

<style>
    .el-menu-vertical-demo:not(.el-menu--collapse) {
        width: 200px;
        min-height: 400px;
    }
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }
  
  .el-aside {
    color: #333;
  }
</style>

<script>
    import ChartView from "../components/ChartView.vue"
    import DocumentView from "../components/DocumentView.vue"
    export default {
    comments: {
        ChartView,
        DocumentView,
    },
    data() {
        return {
            flag:true,
            isCollapse: true,
            isShow:true,
            iconType:"el-icon-s-unfold",
        };
    },
    methods: {
        ToDocument(){
            console.log(1);
            this.flag=false;
        },
        ToCharts(){
            this.flag=true;
        },
        LogOut() {
            this.$router.push("/");
        },
        handleOpen(key, keyPath) {
            console.log(key, keyPath);
        },
        handleClose(key, keyPath) {
            console.log(key, keyPath);
        },
        zhankai(){
            this.isCollapse=!this.isCollapse;
            if(!this.isCollapse)
            this.iconType="el-icon-s-fold";
            else this.iconType="el-icon-s-unfold";

        }
    },
    components: { ChartView, DocumentView }
};
</script>
<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 1.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>