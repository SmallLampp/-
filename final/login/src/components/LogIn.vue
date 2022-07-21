<template>
  <div class="loginBackground">
    <div class="loginBody">
        <div style="margin: 30px;">
            <div class="row" style="">
                <div class="col-md-4">
                    <label for="">
                        <strong>
                            登录账号:  
                        </strong>
                    </label>
                </div>
                <div class="col-md-7">
                    <input type="text" v-model="messageT" class="form-control " placeholder="账号包含数字和下划线" id="ts" >
                </div>
                <div class="col-md-1" >
                    <span @click="clk" class="glyphicon glyphicon-remove-circle" id="fk" style="display:inline-block; cursor:pointer;">
                        <!-- <button class="btn btn-default" type="button">Go!</button> -->
                    </span>
                </div>
            </div>
        </div>
        <div style="margin: 30px;">
            <div class="row" style="">
                <div class="col-md-4">
                    <label for="">
                        <strong>
                            登录密码:  
                        </strong>
                    </label>
                </div>
                <div class="col-md-7">
                    <input :type="eyeType" class="form-control " v-model="messageP" placeholder="输入密码" id="ts" >
                </div>
                <div class="col-md-1" >
                    <span @click="changeEye" :class="eye" id="fk" style="display:inline-block; cursor:pointer;">
                        <!-- <button class="btn btn-default" type="button">Go!</button> -->
                    </span>
                </div>
            </div>
        </div>
        <div style="margin: 30px;">
            <div class="row" style="">
                <div class="col-md-4">
                    <span @click="refreshCode" style="cursor:pointer;">
                        <SIdentify  :identifyCode="identifyCode"></SIdentify>
                    </span>
                </div>
                <div class="col-md-7">
                    <input type="text" v-model="messageY" class="form-control " placeholder="输入验证码" id="ts" >
                </div>
                <div class="col-md-1" >
                    
                </div>
            </div>
        </div>
        <div style="margin: 30px;">
            <div class="row" style="">
                <div class="col-md-4">
                    <button class="bt1" style="padding:0%" @click="switchView"><img src="@/assets/login.jpg" alt="" class="dl" /></button>
                </div>
                <div class="col-md-4" >

                </div>
                <div class="col-md-4">
                    <button @click="chongzhi" class="bt1" style="padding:0%"><img src="@/assets/cz.jpg" alt="" class="dl" /></button>
                </div>
                
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import SIdentify from '../components/identifyUi.vue'
import axios from 'axios'
export default {
    name:"LogIn",
    components:{
        SIdentify,
    },
    
    data(){
        return {
            eye:"glyphicon glyphicon-eye-close",
            flag:-1,
            eyeType:"password",
            ismessageT:false,
            ismessageP:false,
            ismessageY:false,
            messageT:"",
            messageP:"",
            messageY:"",
            identifyCodes:"1234567890",
            // ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz
            identifyCode: "",
            person:{
                // account:"adm_in1",passw:"123456",Yan:this.identifyCode
            },
            validators:{
                account: {
                    message: '用户名错误',
                    ismessageT:false,
                    Answer:"",
                    validate(value) {
                        var re=/(?=.*[\d])(?=.*_)/;
                        if(re.exec(value))
                        {
                            this.message="用户名错误"
                            if(value==this.Answer)this.ismessageT=true;
                            return value==this.Answer ;
                        }
                        else{
                            this.message="账号必须包含数字和下划线"
                        }
                    },
                },
                passw: {
                    ismessageP:false,
                    Answer:"",
                    validate(value) {
                        if(value==this.Answer)this.ismessageP=true;
                        console.log(this.Answer);
                        console.log(value);
                        console.log(value==this.Answer);
                        return value==this.Answer ;
                    },
                    message: '密码错误'
                },
                Yan: {
                    ismessageY:false,
                    Answer:"",
                    validate(value) {
                        if(value==this.Answer)this.ismessageY=true;
                        return value==this.Answer;
                    },
                    message: '验证码错误'
                }
            },
        }
    },
    mounted() {
        this.identifyCode = "";
        this.makeCode(this.identifyCodes, 4);
        // axios.get('/static/account.json')
        //             .then((res) => {
        //                 this.person=res.data.person;
        //         })
        this.initJson();
    },
    created(){
        // this.initJson();
    },
    methods: {
        initJson(){
            axios.get('/static/account.json')
                    .then((res) => {
                        this.person=res.data.person;
                        console.log(res.data.person);
            })
            axios.get('/static/ChartData.json')
                    .then((res) => {
                        // this.initChart();
                        this.$store.commit('saveDbSource',res.data);  
            })
            
            this.validators.account.Answer=this.person.account;
            this.validators.passw.Answer=this.person.passw;
            this.validators.Yan.Answer=this.identifyCode;

            this.$store.commit('saveCurrDbSource',this.person);
        },
        validator(obj, validators) {
            this.initJson();
            return new Proxy(obj, {
                set(target, key, value) {
                    const validator = validators[key]
                    if (!validator) {
                        target[key] = value;
                    } else if (validator.validate(value)) {
                        target[key] = value;
                    } 
                    else 
                    {
                        alert(validator.message || "");
                    }
                    return true;
                }
            })
        },
        switchView(){
            let Personal = {
                account:this.messageT,
                passw:this.messageP,
                Yan:this.messageY,
            }
            Personal = this.validator(Personal, this.validators);

            Personal.account=this.messageT;
            Personal.passw=this.messageP;
            Personal.Yan=this.messageY;


            this.ismessageT=this.validators.account.ismessageT;
            this.ismessageP=this.validators.passw.ismessageP;
            this.ismessageY=this.validators.Yan.ismessageY;

            if(this.ismessageT&&this.ismessageP&&this.ismessageY)
            {
                this.$router.push('/Welcome');
            }
        },
        chongzhi(){
            window.location.reload();
        },
        clk(){
            this.messageT="";
        },
        changeEye(){
            if(this.flag==1)
            {
                this.eye="glyphicon glyphicon-eye-close";
                this.eyeType="password";
            }
            else
            {
                this.eye="glyphicon glyphicon-eye-open";
                this.eyeType="text";
            }
            this.flag=-this.flag;
        },
        refreshCode() {
            this.identifyCode = "";
            this.makeCode(this.identifyCodes, 4);
            this.validators.Yan.Answer=this.identifyCode;
        },
        randomNum(min, max) {
             return Math.floor(Math.random() * (max - min) + min);
        },
        makeCode(o, l) {
            for (let i = 0; i < l; i++) {
                this.identifyCode += this.identifyCodes[
                this.randomNum(0, this.identifyCodes.length)
                ];
            }
        },
    }
};
</script>

<style>
.loginBackground {
  background-image: url("@/assets/dlkk.jpg");
  width: 640px;
  height: 520px;
  background-size: cover;
  position: absolute;
  right: 10%;
  top: 20%;
}

#fk{
    position: absolute;
    right: 140%;
    top:40%;
}
.loginBody {
  width: 600px;
  height: 420px;
  position: absolute;
  left: 40px;
  top: 100px;
}
.bt1{
    border: none;
}
label {
  font-size: 32px;
}
.biaodan div {
    margin: 30px;
    border: 0;
    padding: 0;
}
.biaodan input {
  position: absolute;
  right: 20%;
  width: 300px;
  height: 30px;
}
#ts {
  width: 100%;
  height: 100%;
  font-size: large;
}
.dl {
  width: 100%;
  height: 100%;
}
.cz {
  position: absolute;
  right: 20%;
}
</style>