<template>
  <div class="login-register">
    <div class="contain">
      <div class="big-box" :class="{active: isLogin}">
        <div class="big-contain" v-if="isLogin">
          <div class="btitle">账户登录</div>
          <div class="bform">
            <input type="email" placeholder="邮箱" v-model="form.useremail" @keydown="keyDownEmail">
            <span class="errTips" v-if="emailError">* {{emailPhone}} *</span>
            <input type="password" placeholder="密码" v-model="form.userpwd" @keydown="keyDownPwd">
            <span class="errTips" v-if="pwdError">* {{pwd}} *</span>
          </div>
          <button class="bbutton" @click="login">登录</button>
        </div>
        <div class="big-contain" v-else>
          <div class="btitle">创建账户</div>
          <div class="bform">
            <input type="text" placeholder="用户名" v-model="form.username" @keydown="keyDownName">
            <span class="errTips" v-if="existed,regisNameErr">* {{regisName}} *</span>
            <input type="email" placeholder="邮箱" v-model="form.useremail" @keydown="keyDownRegisEmail">
            <span class="errTips" v-if="regisEmailErr">* {{regisEmail}}*</span>
            <input type="password" placeholder="密码" v-model="form.userpwd" @keydown="keyDownRegisPwd">
            <span class="errTips" v-if="regisPwdErr">* {{regisPwd}} *</span>
          </div>
          <button class="bbutton" @click="register">注册</button>
        </div>
      </div>
      <div class="small-box" :class="{active: isLogin}">
        <div class="small-contain" v-if="isLogin">
          <div class="stitle">你好，朋友!</div>
          <p class="scontent">开始注册，和我们一起旅行</p>
          <button class="sbutton" @click="changeType">注册</button>
        </div>
        <div class="small-contain" v-else>
          <div class="stitle">欢迎回来!</div>
          <p class="scontent">与我们保持联系，请登录你的账户</p>
          <button class="sbutton" @click="changeType">登录</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {PHONEREGULAR} from "@/common/common";
  import {EMAILREGULAR} from "@/common/common";

  export default{
		name:'login-register',
    data() {
		  return {
		    regisName: "用户名不能为空！",
        regisEmail: "邮箱不能为空！",
        regisPwd: "密码不能为空！",
		    emailPhone: "邮箱填写错误",
        pwd: "密码填写错误",
		    isLogin: false,
        emailError: false,
        pwdError: false,
        existed: false,
        regisNameErr: false,
        regisEmailErr: false,
        regisPwdErr: false,
        form: {
		      username: '',
          useremail: '',
          userpwd: ''
        }
      }
    },
    methods: {
      changeType() {
        this.isLogin = !this.isLogin
      },
      login(){
        const useremail = this.form.useremail
        const pwd = this.form.userpwd
        if (useremail === ''){
          this.emailError = true
          this.emailPhone = '邮箱不能为空'
          return
        }else if (pwd === ''){
          this.pwdError = true
          this.pwd = '密码不能为空'
          return
        }

        //正则校验email
        if (EMAILREGULAR.test(useremail)){    //格式正确
          //发送异步请求，传递正确参数进行返回
          alert('登录成功')


        }else {   //格式不正确
          this.emailError = true
          this.emailPhone = '邮箱格式错误'
          return;
        }

      },
      register() {
        const name = this.form.username;
        const email = this.form.useremail;
        const pwd = this.form.userpwd;
        if (name === ''){
          this.regisNameErr = true
          return
        }else if (email === '') {
          this.regisEmailErr = true
          return
        }else if (pwd === '') {
          this.regisPwdErr = true
          return
        }

        //正则校验email
        if (EMAILREGULAR.test(email)){    //格式正确
          //发送异步请求，传递正确参数进行返回
          alert('注册成功，请登录')


        }else {   //格式不正确
          this.regisEmailErr = true
          this.regisEmail = "邮箱格式不正确！"
        }
      },
      keyDownEmail() {
        this.emailError = false;
      },
      keyDownPwd() {
        this.pwdError = false;
      },
      keyDownName() {
        this.regisNameErr = false;
      },
      keyDownRegisEmail() {
        this.regisEmailErr = false;
      },
      keyDownRegisPwd() {
        this.regisPwdErr = false;
      },
    },
	}
</script>

<style scoped="scoped">
  .login-register {
    width: 100vw;
    height: 100vh;
    box-sizing: border-box;
  }
  .contain {
    width: 60%;
    height: 60%;
    position: relative;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    border-radius: 20px;
    box-shadow: 0 0 3px #f0f0f0,
    0 0 6px #f0f0f0;
  }
  .big-box {
    width: 70%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 30%;
    transform: translatex(0%);
    transition: all 1s;
  }
  .small-box {
    width: 30%;
    height: 100%;
    background: linear-gradient(135deg,rgb(57,167,176),rgb(56,183,145));
    position: absolute;
    top: 0;
    left: 0;
    transform: translateX(0%);
    transition: all 1s;
    border-top-left-radius: inherit;
    border-bottom-left-radius: inherit;
  }
  .big-box.active {
    left: 0;
    transition: all 0.5s;
  }
  .small-box.active {
    left: 100%;
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
    border-top-right-radius: inherit;
    border-bottom-right-radius: inherit;
    transform: translateX(-100%);
    transition: all 1s;
  }
  .big-contain {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .btitle{
    font-size: 1.5em;
    font-weight: bold;
    color: rgb(57,167,176);
  }
  .bform{
    width: 100%;
    height: 40%;
    padding: 2em 0;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
  }
  .bform input{
    width: 50%;
    height: 30px;
    border: none;
    outline: none;
    border-radius: 10px;
    padding-left: 2em;
    background-color: #f0f0f0;
  }
  .bform .errTips{
    display: block;
    width: 50%;
    text-align: left;
    color: red;
    font-size: 0.7em;
    margin-left: 1em;
  }
  .bbutton{
    width: 20%;
    height: 40px;
    border-radius: 24px;
    border: none;
    outline: none;
    background-color: rgb(57,167,176);
    color: #fff;
    font-size: 0.9em;
    cursor: pointer;
  }
  .small-contain{
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .stitle{
    font-size: 1.5em;
    font-weight: bold;
    color: #fff;
  }
  .scontent{
    font-size: 0.8em;
    color: #fff;
    text-align: center;
    padding: 2em 4em;
    line-height: 1.7em;
  }
  .sbutton{
    width: 60%;
    height: 40px;
    border-radius: 24px;
    border: 1px solid #fff;
    outline: none;
    background-color: transparent;
    color: #fff;
    font-size: 0.9em;
    cursor: pointer;
  }
</style>
