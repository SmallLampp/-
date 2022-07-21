<template>
    <div>
        <div id="mainB" style="width: 700px;height:400px;display:inline;float:left;margin-right: 150px;"></div>
        <div id="mainZhu" style="width: 700px;height:400px;display:inline;float:left;"></div>
        <div id="mainZ" style="width: 700px;height:400px;display:inline;float:left;"></div>
        <div class="changeData">
            <el-dropdown>
                <el-button type="primary">
                    选择课程<i class="el-icon-arrow-down el-icon--right"></i>
                </el-button>
                <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item @click.native="ToMath">数学</el-dropdown-item>
                    <el-dropdown-item @click.native="ToChinese">语文</el-dropdown-item>
                    <el-dropdown-item @click.native="ToEnglish">英语</el-dropdown-item>
                </el-dropdown-menu>
            </el-dropdown>
        </div>
     </div>  
</template>
<script>
import * as echarts from 'echarts';
import axios from 'axios'
    export default{
        mounted(){
            // this.initChart();
        },
        updated(){
            // this.initChart()
        },
        created(){
            this.initData();
            // console.log('参数数据',this.$store.state.DbSource.optionBMa);
            // this.initChart()
        },
        data(){
            return {
                radio: 3,
                myChartZhu:{
                    
                },
                myChartB:{
                    
                },
                myChartZ:{
                    
                }
            }
        },
        methods:{
            initChart(){

                var chartDomB = document.getElementById('mainB');
                this.myChartB = echarts.init(chartDomB);
                console.log(this.$store.state.DbSource.optionBMa);
                this.$store.state.DbSource.optionBMa && this.myChartB.setOption(this.$store.state.DbSource.optionBMa);
                // this.myChartB.refresh();
                // console.log(this.$store.state.DbSource.optionBMa);

                var chartDomZhu = document.getElementById('mainZhu');
                this.myChartZhu = echarts.init(chartDomZhu);
                this.$store.state.DbSource.optionZhuMa && this.myChartZhu.setOption(this.$store.state.DbSource.optionZhuMa);
                // this.myChartZhu.refresh();

                var chartDomZ = document.getElementById('mainZ');
                this.myChartZ = echarts.init(chartDomZ);
                this.$store.state.DbSource.optionZMa && this.myChartZ.setOption(this.$store.state.DbSource.optionZMa);
                // this.myChartZ.refresh();

                this.myChartB.group='group1';
                this.myChartZ.group='group1';
                this.myChartZhu.group='group1';
                echarts.connect('group1');
                console.log(this.$store.state.DbSource.optionBMa);
            },
            initData(){
                axios.get('/static/ChartData.json')
                    .then((res) => {
                        this.initChart();
                        this.$store.commit('saveDbSource',res.data);
                        
                })
            },
            ToEnglish(){
                this.myChartZhu.setOption(this.$store.state.DbSource.optionZhuEn);
                this.myChartZ.setOption(this.$store.state.DbSource.optionZEn);
                this.myChartB.setOption(this.$store.state.DbSource.optionBEn);
            },
            ToMath(){
                this.myChartZhu.setOption(this.$store.state.DbSource.optionZhuMa);
                this.myChartZ.setOption(this.$store.state.DbSource.optionZMa);
                this.myChartB.setOption(this.$store.state.DbSource.optionBMa);
            },
            ToChinese(){
                this.myChartZhu.setOption(this.$store.state.DbSource.optionZhuCh);
                this.myChartZ.setOption(this.$store.state.DbSource.optionZCh);
                this.myChartB.setOption(this.$store.state.DbSource.optionBCh);
            }
        }
    }
    
</script>
<style>
.changeData{
    position: absolute;
    bottom: 20%;
    right: 30%;
}

</style>