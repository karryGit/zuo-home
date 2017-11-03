<template>
  <div>

    <!--全局容器-->
    <header id="zuo-content-container">
      <!--头部标题部分-->
      <header id="zuo-header" v-show="isShow">
        <div class="welcome-body">
          <h3>可能是全宇宙最ZUO的图片社区</h3>
          <div class="subtip">
            <span class="subtip1">和像你一样认真对待生活的人一起</span>
            <br>
            <span class="subtip2">从设计的视角，重新认识世界</span>
          </div>
          <button id="new-zuoer-link"><a href="logon.html">创建ZUO账号</a></button>
        </div>
        <div class="close" @click="hide">
          <img src="../../assets/close1.png"/>
        </div>
      </header>
    </header>
  </div>
</template>
<script>

  export default {
    name: 'Index',
    data() {
      return {
        isShow: true
      }
    },
    methods: {
      hide() {
        this.isShow = false;
      }
    }
  }
</script>

<style scoped>
  body {
    width: 100%;
    background-color: rgb(246, 246, 246);
  }

  #zuo-content-container {
    padding-top: 40px;
  }

  #zuo-header {
    width: 100%;
    height: 250px;
    background: url("../../assets/bg.png") no-repeat;
    position: relative;
    background-repeat: repeat;
    background-color: #eaeced;
  }

  .welcome-body {
    width: 790px;
    margin: 10px auto;
    text-align: center;
    padding-top: 30px;
    padding-bottom: 30px;
  }

  .welcome-body h1 {
    font-size: 24px;
    margin: 0;
    font-weight: 700;
    color: #272c2f;
  }

  .subtip {
    margin-top: 15px;
    margin-bottom: 18px;
    font-size: 16px;
    color: #5d6c75;
  }

  #new-zuoer-link {
    height: 50px;
    border: none;
    width: 200px;
    font-size: 16px;
    background-color: #1fd7e2;
    color: #fff;
  }

  #new-zuoer-link a {
    color: white;
  }

  .close {
    position: absolute;
    display: block;
    width: 20px;
    height: 20px;
    top: 18%;
    right: 2.8%;
  }
</style>
