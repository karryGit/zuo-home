<template>
  <!--注册弹出页面-->
  <div id="zuo-logon">
    <div class="zuo-overlay" @click="maskClick">
      <!--登录header-->
      <div class="zuo-login-con-container">
        <div class="login-header">
          <img src="../../assets/zhuomoniao.png"/>
          <span class="title-text">
              <strong>ZUO</strong>&nbsp;&nbsp;
              欢迎你的加入
            </span>
        </div>
        <!--登录内容-->
        <div class="login-content1">
          <div class="close">
            <a href="index.html"> <img src="../../assets/close.png"/></a>
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
            <input @focus="phoneFocus" :style="{border:isBorder}" class="zuo-phone" v-model="username" type="text"
                   placeholder="手机号">
            <img v-show="isTestShow" class="fillWrite1" src="../../assets/images/请填写验证码.png"/>
            <input class="zuo-captcha" :style="{border:isBorder1}" @focus="testCodeFocus" v-model="testCodeValue"
                   type="text" placeholder="验证码">
            <button class="send1" @click="sendClick">发送验证码</button>
            <img v-show="isPassShow" class="pass" src="../../assets/images/密码长度不小于6.png"/>
            <input @focus="passFocus" :style="{border:isBorder2}" class="password" v-model="password" type="password"
                   placeholder="密码">
            <img v-show="isNewPassShow" class="confirm" src="../../assets/images/两次密码不一致.png"/>
            <input :style="{border:isBorder3}" @focus="repassFocus" class="confirmPassword" v-model="affirmPass"
                   type="password" placeholder="确认密码">
          </div>
          <!--已有账号去登录-->
          <div class="other-actions1">
            <img @click="checkLogon" class="checked" :src="isSrc ? srcChecked:srcChecked1"/>
            <span class="policy-tip">我已经认真阅读并同意<strong>ZUO</strong>的</span>
            <a id="login-link" href="login.html">已有账号，登录</a>
            <a class="agree" href="http://zuoooodesign.lofter.com/post/1d1a2c6b_6478482" target="_blank">《用户协议》</a>
          </div>
          <button @click="loginIng" :class="isLogin ? login1 : login2" :disabled="isDisabled">注册</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import axios from 'axios';

  export default {
    name: 'logon',
    data() {
      return {
        srcChecked: require('../../assets/icon_home_checkbox.png'),
        srcChecked1: require('../../assets/icon_home_checkbox (1).png'),
        isSrc: true,
        isLogin: true,
        login1: 'zuo-login-btn1',
        login2: 'zuo-login-btn2',
        isDisabled: false,
        username: '',
        testCodeValue: '',
        password: '',
        affirmPass: '',
        isFill: false,
        fillWriteSrc: require('../../assets/images/请填写手机号.png'),
        isBorder: '',
        isBorder1: '',
        isBorder2: '',
        isBorder3: '',
        isTestShow: false,
        isPassShow: false,
        isNewPassShow: false
      }
    },
    methods: {
      checkLogon() {
        this.isSrc = !this.isSrc
        if (this.isSrc == false) {
          this.isLogin = false;
          this.isDisabled = true;
        } else {
          this.isLogin = true;
          this.isDisabled = false;
        }
      },
      loginIng() {
        //判断账号是否为空
        if (this.username.length == 0) {
          this.isFill = true;
          this.isBorder = '1px solid red';
          return;//不提交
        }
        //判断是否是一个手机号
        let re = /^1[34578][0-9]{9}$/g;//不加0的
        if (!re.test(this.username)) {
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
        if (this.password.length < 6) {
          this.isBorder2 = '1px solid red';
          this.isPassShow = true;
          return
        }
        //判断新密码和确认密码是否一致
        if (this.password !== this.affirmPass) {
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
      sendClick() {
        //判断账号是否为空
        if (this.username.length == 0) {
          this.isFill = true;
          this.isBorder = '1px solid red';
          return;//不提交
        }
        //判断是否是一个手机号
        let re = /^1[34578][0-9]{9}$/g;//不加0的
        if (!re.test(this.username)) {
          this.isBorder = '1px solid red';
          this.isFill = true;
          this.fillWriteSrc = require('../../assets/images/手机号码格式不正确.png');
          return;//不提交
        }
      },
      maskClick() {
        window.location.href = 'index.html';
      }
    },
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

  /*注册弹出部分*/
  .zuo-overlay {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    width: 100%;
    height: 100%;
    z-index: 3000;
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
    right: -185px;
    top: 3%;
  }

  .fillWrite1 {
    position: absolute;
    right: -185px;
    top: 30%;
  }

  .pass {
    position: absolute;
    right: -185px;
    top: 55%;
  }

  .confirm {
    position: absolute;
    right: -185px;
    top: 85%;
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

  .close {
    width: 18px;
    height: 18px;
    position: absolute;
    right: -6%;
    top: -17%;

  }
</style>
