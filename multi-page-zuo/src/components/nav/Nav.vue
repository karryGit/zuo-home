<template>
  <div>
    <!--导航栏-->
    <nav id="zuo-nav">
      <!--导航栏容器-->
      <nav id="container">
        <!--左边部分-->
        <div class="zuo-nav-left float-left">
          <a href="index.html" class="zuo-brand clear_float">
            <p class="logo float-left">ZUO</p>
            <p class="logo_span float-left"> HONEY WASABI </p>
          </a>
        </div>
        <!--中间部分-->
        <div class="zuo-nav-right float-left">
          <ul class="zuo-nav-right-left float-left">
            <li v-for="(header,index) in headers" :key="index" :index="index" @click="table(index)">
              <a :href="header.href" :class="header.active">{{header.title}}</a>
            </li>
          </ul>
          <!--搜索框-->
          <div class="zuo-nav-right-centre float-left">
            <input class="zuo-nav-right-centre_search" type="text" placeholder="输入关键字搜索">
            <a href="#" class="zuo-nav-right-centre_a">
              <img class="zuo-nav-right-centre-img" src="../../assets/sousuo.png"/>
            </a>
          </div>
          <!--登录注册部分-->
          <div class="zuo-nav-right-right float-right">
            <ul class="zuo-nav-right-right-ul">
              <li class="zuo-nav-right-right-login" @click="login">
                <img src="../../assets/denglu.png"/>
                <a href="login.html"><span>登录</span></a>
              </li>
              <li class="zuo-nav-right-right-logon" @click="logon">
                <a href="logon.html"><span>注册</span></a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </nav>
    <!--&lt;!&ndash;登录弹出页面&ndash;&gt;-->
    <!--<div v-show="isShow" id="zuo-login">-->
      <!--<div class="zuo-overlay">-->
        <!--&lt;!&ndash;登录header&ndash;&gt;-->
        <!--<div class="zuo-login-con-container">-->
          <!--<div class="login-header">-->
            <!--<img src="../../assets/zhuomoniao.png"/>-->
            <!--<span class="title-text">欢迎回到&nbsp;&nbsp;-->
              <!--<strong>ZUO</strong>-->
            <!--</span>-->
          <!--</div>-->
          <!--&lt;!&ndash;登录内容&ndash;&gt;-->
          <!--<div class="login-content">-->
            <!--<div class="close" @click="close">-->
              <!--<img src="../../assets/close.png"/>-->
            <!--</div>-->
            <!--<img class="weibo" src="../../assets/weibo.png"/>-->
            <!--<img class="weixin" src="../../assets/weixin.png"/>-->
            <!--<p class="social">你可以使用第三方社交账号直接登录</p>-->
            <!--<div class="hengxian-wrap">-->
              <!--<div class="hengxian1"></div>-->
              <!--<div class="or">或者</div>-->
              <!--<div class="hengxian2"></div>-->
            <!--</div>-->
            <!--<div class="zuo-send">-->
              <!--<input class="zuo-phone" type="text" placeholder="手机号">-->
              <!--<input class="zuo-captcha" type="text" placeholder="验证码">-->
              <!--<button class="send">发送验证码</button>-->
            <!--</div>-->
            <!--&lt;!&ndash;没有账号?去注册&ndash;&gt;-->
            <!--<div class="other-actions">-->
              <!--<a class="sign-up-link">没有账号？去注册</a>-->
              <!--<a class="pass-login-link">-->
                <!--<img class="lock" src="../../assets/lock.png"/>-->
                <!--<span>手机密码登录</span>-->
              <!--</a>-->
            <!--</div>-->
            <!--<button class="zuo-login-btn">登录</button>-->
          <!--</div>-->
        <!--</div>-->
      <!--</div>-->
    <!--</div>-->
    <!--&lt;!&ndash;注册弹出页面&ndash;&gt;-->
    <!--<div v-show="isLogon ? 'key': ''" id="zuo-logon">-->
      <!--<div class="zuo-overlay">-->
        <!--&lt;!&ndash;登录header&ndash;&gt;-->
        <!--<div class="zuo-login-con-container">-->
          <!--<div class="login-header">-->
            <!--<img src="../../assets/zhuomoniao.png"/>-->
            <!--<span class="title-text">-->
              <!--<strong>ZUO</strong>&nbsp;&nbsp;-->
              <!--欢迎你的加入-->
            <!--</span>-->
          <!--</div>-->
          <!--&lt;!&ndash;登录内容&ndash;&gt;-->
          <!--<div class="login-content1">-->
            <!--<div class="close" @click="close">-->
              <!--<img src="../../assets/close.png"/>-->
            <!--</div>-->
            <!--<img class="weibo" src="../../assets/weibo.png"/>-->
            <!--<img class="weixin" src="../../assets/weixin.png"/>-->
            <!--<p class="social">你可以使用第三方社交账号直接登录</p>-->
            <!--<div class="hengxian-wrap">-->
              <!--<div class="hengxian1"></div>-->
              <!--<div class="or">或者</div>-->
              <!--<div class="hengxian2"></div>-->
            <!--</div>-->
            <!--<div class="zuo-send">-->
              <!--<input class="zuo-phone" type="text" placeholder="手机号">-->
              <!--<input class="zuo-captcha" type="text" placeholder="验证码">-->
              <!--<button class="send1">发送验证码</button>-->
              <!--<input class="password" type="password" placeholder="密码">-->
              <!--<input class="confirmPassword" type="password" placeholder="确认密码">-->
            <!--</div>-->
            <!--&lt;!&ndash;已有账号去登录&ndash;&gt;-->
            <!--<div class="other-actions1">-->
              <!--<img @click="checkLogon" class="checked" :src="isSrc ? srcChecked:srcChecked1"/>-->
              <!--<span class="policy-tip">我已经认真阅读并同意<strong>ZUO</strong>的</span>-->
              <!--<a id="login-link">已有账号，登录</a>-->
              <!--<a class="agree" href="http://zuoooodesign.lofter.com/post/1d1a2c6b_6478482" target="_blank">《用户协议》</a>-->
            <!--</div>-->
            <!--<button :class="isLogin ? login1 : login2" :disabled="isDisabled">注册</button>-->
          <!--</div>-->
        <!--</div>-->
      <!--</div>-->
    <!--</div>-->
  </div>
</template>
<script>
  import axios from 'axios';

  export default {
    name: 'nav',
    data() {
      return {
        isShow: false,
        isLogon: false,
        srcChecked: require('../../assets/icon_home_checkbox.png'),
        srcChecked1: require('../../assets/icon_home_checkbox (1).png'),
        isSrc: true,
        isLogin: true,
        login1: 'zuo-login-btn1',
        login2: 'zuo-login-btn2',
        isDisabled: false,
        headers: [
          {title: '首页', href: 'index.html', active: 'active'},
          {title: '深度', href: 'depth.html', active: ''},
          {title: '下载APP', href: 'downloadApp.html', active: ''}
        ]
      }
    },
    methods: {
      close() {
        this.isShow = false;
        this.isLogon = false;
      },
      login() {
        this.isShow = true;
      },
      logon() {
        this.isLogon = true;
      },
      table(index) {
        for (var i = 0; i < this.headers.length; i++) {
          this.headers[i].active = '';
          this.headers[index].active = 'active';
        }
      },
      checkLogon() {
        this.isSrc = !this.isSrc
        if (this.isSrc == false) {
          this.isLogin = false;
          this.isDisabled = true;
        } else {
          this.isLogin = true;
          this.isDisabled = false;
        }
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

  #zuo-nav {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 3000;
    width: 100%;
    height: 60px;
    background-color: rgb(39, 44, 47);
  }

  #container {
    width: 1200px;
    margin: 0 auto;
  }

  .zuo-nav-left {
    width: 30%;
  }

  .zuo-nav-right {
    width: 70%;
  }

  .zuo-nav-right ul li {
    line-height: 60px;
    float: left;
    list-style: none;
    margin-left: 26px;

  }

  .zuo-nav-right ul li a {
    color: rgb(127, 127, 127);
    font-size: 14px;
    text-decoration: none;
  }

  .zuo-nav-right ul li .active {
    color: white;
  }

  .zuo-nav-left a {
    line-height: 60px;
    color: white;
    text-decoration: none;
  }

  .zuo-nav-right-centre {
    position: relative;
    margin-left: 40px;
    line-height: 60px;
  }

  .zuo-nav-right-centre_search {
    font-size: 12px;
    background-color: rgb(75, 80, 82);
    border: none;
    outline: none;
    border-radius: 5px;
    width: 240px;
    padding-left: 10px;
    height: 36px;
  }

  .logo {
    font-weight: 800;
    font-size: 20px;
  }

  .logo_span {
    margin-left: 5px;
    font-size: 10px;
    color: rgba(255, 255, 255, .3);
    width: 100px;
  }

  .zuo-nav-right-left {
    padding-left: 43px;
  }

  .zuo-nav-right-centre-img {
    position: absolute;
    left: 86%;
    top: 36%;
    width: 20px;
    height: 20px;
  }

  .zuo-nav-right-right-login {
    width: 40px;
    height: 60px;
    position: relative;
  }

  .zuo-nav-right-right img {
    position: absolute;
    left: -25px;
    top: 18px;
    width: 25px;
    height: 25px;
  }

  .zuo-nav-right-right-ul span {
    font-size: 13px;
    color: rgb(151, 160, 165);
  }

</style>
