<template>
  <!--登录弹出页面-->
  <div id="zuo-login">
    <div class="zuo-overlay" @click="maskClick">
      <!--登录header-->
      <div class="zuo-login-con-container" v-show="isLoginShow">
        <div class="login-header">
          <img src="../../assets/zhuomoniao.png"/>
          <span class="title-text">欢迎回到&nbsp;&nbsp;
              <strong>ZUO</strong>
            </span>
        </div>
        <!--登录内容-->
        <div class="login-content">
          <div class="close">
            <a href="index.html"><img src="../../assets/close.png"/></a>
          </div>
          <img class="weibo" src="../../assets/weibo.png"/>
          <img class="weixin" src="../../assets/weixin.png"/>
          <p class="social">你可以使用第三方社交账号直接登录</p>
          <div class="hengxian-wrap">
            <div class="hengxian1"></div>
            <div class="or">或者</div>
            <div class="hengxian2"></div>
          </div>
          <div class="zuo-send">
            <img v-show="isFill" class="fillWrite" :src="fillWriteSrc"/>
            <input class="zuo-phone" @focus="phoneFocus" :style="{border:isBorder}" v-model="phoneValue" type="text"
                   placeholder="手机号">
            <img v-show="isTestShow" class="fillWrite3" src="../../assets/images/请填写验证码.png"/>
            <input @focus="testCodeFocus" class="zuo-captcha" type="text" v-model="testCodeValue"
                   :placeholder="testCode" :style="{border:isBorder1}">
            <button v-show="isLogin" @click="sendClick" class="send">发送验证码</button>
          </div>
          <!--没有账号?去注册-->
          <div class="other-actions">
            <a class="sign-up-link" @click="forgetClick">{{forget}}</a>
            <a class="pass-login-link" v-show="isLock" @click="lockClick">
              <img class="lock" src="../../assets/lock.png"/>
              <span>手机密码登录</span>
            </a>
            <a class="pass-login-link" v-show="isPhone" @click="lockClick">
              <img class="lock" src="../../assets/images/手机.png"/>
              <span>手机验证码登录</span>
            </a>
          </div>
          <button class="zuo-login-btn" @click="checkLogin">登录</button>
        </div>
      </div>
      <!--忘记密码部分-->
      <div class="auth-box" v-show="isForgetPassWord">
        <div class="closeForget">
          <a href="index.html"><img src="../../assets/close.png"/></a>
        </div>
        <div class="auth-box-body">
          <header class="box-title">忘记密码</header>
          <div class="form-wrap">
            <div class="form-body">
              <div class="zuo-form">
                <div class="zuo-control-group">
                  <img v-show="isFill" class="fillWrite1" :src="fillWriteSrc"/>
                  <input type="text" name="phone" @focus="phoneFocus" :style="{border:isBorder}" v-model="phoneValue"
                         placeholder="手机号" class="zuo-control">
                </div>
                <div class="zuo-control-group">
                  <img v-show="isTestShow" class="fillWrite2" src="../../assets/images/请填写验证码.png"/>
                  <input id="code" type="text" name="code" @focus="testCodeFocus" v-model="testCodeValue"
                         placeholder="验证码" class="zuo-control" :style="{border:isBorder1}">
                  <button id="zuo-get-code" class="zuo-btn zuo-btn-theme">发送验证码</button>
                </div>
                <div class="zuo-control-group">
                  <img v-show="isPassShow" class="pass" src="../../assets/images/密码长度不小于6.png"/>
                  <input type="password" name="password" @focus="passFocus" :style="{border:isBorder2}"
                         v-model="newPassValue" placeholder="新密码" class="zuo-control">
                </div>
                <div class="zuo-control-group">
                  <img v-show="isNewPassShow" class="confirm" src="../../assets/images/两次密码不一致.png"/>
                  <input type="password" name="repass" @focus="repassFocus" v-model="confirmValue" placeholder="新密码确认"
                         :style="{border:isBorder3}" class="zuo-control">
                </div>
              </div>
              <div class="actions">
                <button id="forget-pass-submit" class="zuo-btn zuo-btn-theme zuo-btn-block" @click="checkLogin">确认修改
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'login',
    data() {
      return {
        isLock: true,
        isPhone: false,
        isLogin: true,
        forget: '没有账号？去注册',
        testCode: '验证码',
        phoneValue: '',
        isBorder: '',
        isBorder1: '',
        isBorder2: '',
        isBorder3: '',
        isFill: false,
        fillWriteSrc: require('../../assets/images/请填写手机号.png'),
        isLoginShow: true,
        isForgetPassWord: false,
        testCodeValue: '',
        isTestShow: false,
        newPassValue: '',
        isPassShow: false,
        confirmValue: '',
        isNewPassShow: false
      }
    },
    methods: {
      checkLogin() {
        //判断手机号输入是否为空
        if (this.phoneValue.length == 0) {
          this.isBorder = '1px solid red';
          this.isFill = true;
          return;
        }
        //判断是否是一个手机号
        let re = /^1[34578][0-9]{9}$/g;//不加0的
        if (!re.test(this.phoneValue)) {
          this.isBorder = '1px solid red';
          this.isFill = true;
          this.fillWriteSrc = require('../../assets/images/手机号码格式不正确.png');
          return;//不提交
        }
        //判断验证码是否为空
        if (this.testCodeValue.length == 0) {
          this.isBorder1 = '1px solid red';
          this.isTestShow = true;
          return;
        }
        //判断新密码是否为空并且长度不小于6
        if (this.newPassValue.length < 6) {
          this.isBorder2 = '1px solid red';
          this.isPassShow = true;
          return
        }
        //判断新密码和确认密码是否一致
        if (this.newPassValue !== this.confirmValue) {
          this.isBorder3 = '1px solid red';
          this.isNewPassShow = true;
          return
        }
      },
      phoneFocus() {
        this.isBorder = '';
        this.isFill = false;
      },
      testCodeFocus() {
        this.isBorder1 = '';
        this.isTestShow = false;
      },
      passFocus() {
        this.isBorder2 = '';
        this.isPassShow = false;
      },
      repassFocus() {
        this.isBorder3 = '';
        this.isNewPassShow = false;
      },
      lockClick() {
        this.isLock = !this.isLock;
        this.isPhone = !this.isPhone;
        this.isLogin = !this.isLogin;
        if (this.forget == '没有账号？去注册') {
          this.forget = '忘记密码'
        } else {
          this.forget = '没有账号？去注册';
        }
        ;
        if (this.testCode == '验证码') {
          this.testCode = '密码'
        } else {
          this.testCode = '验证码'
        }
      },
      forgetClick() {
        if (this.forget == '没有账号？去注册') {
          window.location.href = 'logon.html'
        }
        if (this.forget == '忘记密码') {
          this.isLoginShow = false;
          this.isForgetPassWord = true;
        }
      },
      sendClick(){
        //判断手机号输入是否为空
        if (this.phoneValue.length == 0) {
          this.isBorder = '1px solid red';
          this.isFill = true;
          return;
        }
        //判断是否是一个手机号
        let re = /^1[34578][0-9]{9}$/g;//不加0的
        if (!re.test(this.phoneValue)) {
          this.isBorder = '1px solid red';
          this.isFill = true;
          this.fillWriteSrc = require('../../assets/images/手机号码格式不正确.png');
          return;//不提交
        }
      },
      maskClick() {
        window.location.href = 'index.html';
      }
    }
  }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
  /*浮动左*/
  .float-left {
    float: left;
  }

  /*浮动右*/
  .float-right {
    float: right;
  }

  /*清除浮动必须加到父级元素上*/
  .clear_float::after {
    content: "";
    display: table;
    clear: both;
  }

  /*忘记密码部分*/
  .auth-box button, input {
    outline: none;
    border: none;
  }

  .auth-box {
    width: 540px;
    position: absolute;
    top: 100px;
    left: 50%;
    margin-left: -270px;
  }

  .closeForget {
    position: absolute;
    display: block;
    width: 20px;
    height: 20px;
    top: 1%;
    right: -6.2%;
  }

  .auth-box-body .box-title {
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    background-color: #272c2f;
    font-size: 18px;
    padding-top: 25px;
    padding-bottom: 25px;
    color: #fff;
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
  }

  .form-body {
    padding-top: 30px;
  }

  .zuo-control-group {
    position: relative;
    margin-bottom: 20px;
  }

  .zuo-control-group {
    position: relative;
    margin-bottom: 20px;
  }

  .pass {
    position: absolute;
    right: -240px;
    top: 10%;
  }

  .confirm {
    position: absolute;
    right: -240px;
    top: 25%;
  }

  .auth-box-body .form-wrap {
    padding: 30px;
    background-color: #fff;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
  }

  .zuo-control-group {
    position: relative;
    margin-bottom: 20px;
  }

  .zuo-control-group input.zuo-control {
    width: 100%;
    background-color: #f7f7f7;
    padding: 14px 20px;
    font-size: 14px;
    line-height: 22px;
  }

  .zuo-btn-theme {
    background-color: #1fd7e2;
    color: #fff;
  }

  .auth-box-body button.zuo-btn-theme {
    font-size: 18px;
  }

  .zuo-btn-block {
    width: 100%;
  }

  .zuo-control-group #zuo-get-code {
    width: 115px;
    position: absolute;
    top: 4px;
    right: 4px;
    padding: 12px 18px;
    font-size: 14px;
  }

  /*登录弹出部分*/
  .zuo-overlay {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    width: 100%;
    height: 100%;
    z-index: 3900;
    background-color: rgba(39, 44, 47, .9);
    background-image: linear-gradient(to top, rgba(39, 44, 47, .9), rgba(39, 44, 47, .5));
    overflow-y: auto;
  }

  .zuo-login-con-container {
    border-radius: 5px;
    width: 540px;
    position: absolute;
    top: 100px;
    left: 50%;
    margin-left: -270px;
    background-color: white;
  }

  .login-header {
    border-top-right-radius: 4px;
    border-top-left-radius: 4px;
    width: 100%;
    height: 80px;
    background-color: #272c2f;
  }

  .login-header img {
    position: absolute;
    left: 36%;
    top: 5%;
    width: 30px;
    height: 30px;
  }

  .title-text {
    position: absolute;
    left: 43%;
    top: 5.5%;
    color: white;
  }

  .login-content {
    width: 100%;
    height: 364px;
    position: relative;
  }

  .login-content1 {
    width: 100%;
    height: 564px;
    position: relative;
  }

  .weibo {
    width: 30px;
    height: 30px;
    position: absolute;
    left: 40%;
    top: 5%;
  }

  .weixin {
    width: 30px;
    height: 30px;
    position: absolute;
    left: 55%;
    top: 5%;
  }

  .social {
    position: absolute;
    left: 33%;
    top: 15%;
    color: rgb(166, 167, 167);
    font-size: 13px;
  }

  .hengxian-wrap {
    position: relative;
    left: 39%;
    top: 26%;
  }

  .hengxian1 {
    width: 130px;
    height: 1px;
    background-color: rgb(215, 216, 216);
    position: absolute;
    left: -21%;
    top: 40%;
  }

  .hengxian2 {
    width: 130px;
    height: 1px;
    background-color: rgb(215, 216, 216);
    position: absolute;
    left: 21%;
    top: 40%;
  }

  .or {
    position: absolute;
    left: 10%;
    top: -9px;
    color: rgb(223, 217, 216);
    font-size: 13px;
  }

  .zuo-send {
    position: relative;
    left: 5%;
    top: 30%;
  }

  .fillWrite {
    position: absolute;
    right: -180px;
    top: 6px;
  }

  .fillWrite1 {
    position: absolute;
    right: -240px;
    top: 10px;
  }

  .fillWrite2 {
    position: absolute;
    right: -240px;
    top: 10px;
  }

  .fillWrite3 {
    position: absolute;
    right: -180px;
    top: 70px;
  }

  .zuo-phone {
    width: 90%;
    height: 45px;
    padding-left: 20px;
    outline: none;
    background-color: rgb(241, 241, 241);
    border: none;
    font-size: 12px;
  }

  .password {
    margin-top: 20px;
    width: 90%;
    height: 45px;
    padding-left: 20px;
    outline: none;
    background-color: rgb(241, 241, 241);
    border: none;
    font-size: 12px;
  }

  .confirmPassword {
    margin-top: 20px;
    width: 90%;
    height: 45px;
    padding-left: 20px;
    outline: none;
    background-color: rgb(241, 241, 241);
    border: none;
    font-size: 12px;
  }

  .zuo-captcha {
    margin-top: 20px;
    width: 90%;
    height: 45px;
    padding-left: 20px;
    outline: none;
    background-color: rgb(241, 241, 241);
    border: none;
    font-size: 12px;
  }

  .send {
    position: absolute;
    right: 10.5%;
    padding: 11px 18px;
    top: 61.5%;
    background-color: rgb(9, 216, 225);
    border: none;
    font-size: 14px;
  }

  .send1 {
    position: absolute;
    right: 10.5%;
    padding: 11px 18px;
    top: 28.0%;
    background-color: rgb(9, 216, 225);
    border: none;
    font-size: 14px;
  }

  .other-actions {
    position: relative;
    left: 6%;
    top: 34%;
  }

  .other-actions a {
    text-decoration: none;
  }

  .other-actions1 {
    font-size: 13px;
    position: relative;
    left: 6%;
    top: 35%;
  }

  .checked {
    position: relative;
    top: 2px;
    width: 15px;
    height: 14px;
  }

  .sign-up-link {
    color: rgb(167, 167, 167);
    font-size: 14px;
    position: absolute;
  }

  #login-link {
    color: rgb(39, 44, 47);
    font-size: 13px;
    position: absolute;
    right: 11%;
    top: -3%;
  }

  .agree {
    color: #1fd7e2;
  }

  .pass-login-link {
    font-size: 14px;
    color: black;
    position: absolute;
    right: 11%;
  }

  .zuo-login-btn {
    border: none;
    background-color: rgb(9, 216, 225);
    position: relative;
    left: 5%;
    top: 195px;
    width: 90%;
    height: 45px;
  }

  .zuo-login-btn1 {
    border: none;
    background-color: rgb(9, 216, 225);
    position: relative;
    left: 5%;
    top: 235px;
    width: 90%;
    height: 45px;
  }

  .zuo-login-btn2 {
    border: none;
    background-color: rgba(9, 216, 225, 0.5);
    position: relative;
    left: 5%;
    top: 235px;
    width: 90%;
    height: 45px;
  }

  .lock {
    position: absolute;
    right: 104%;
    width: 20px;
    height: 20px;
  }

  .close {
    width: 18px;
    height: 18px;
    position: absolute;
    right: -6%;
    top: -17%;
  }

</style>
