<template>
  <div class="recommend-users">
    <header class="side-title"> 推荐关注 </header>
    <div class="users-list" v-for="(recoUser,index) in recoUsers" :key="index" :index="index">
      <div class="user-item">
        <div class="user-text-info">
          <div class="user-name">
            <a href="">{{recoUser.username}}</a>
          </div>
          <div class="user-intro">
            <a href="">{{recoUser.introduction}}</a>
          </div>
        </div>
        <div class="user-avatar">
          <a :title="recoUser.nickname" href="#" @mouseenter="imgEnter(index)" @mouseleave="imgLeave(index)">
            <div class="" ref="mask">
            </div>
            <img alt="" class="zuo-img-rounded" :src="recoUser.avatar">
          </a>
        </div>
      </div>
    </div>
    <!--下载iOS-->
    <div class="download-wrap">
      <div class="download-ios clear_float" @mouseenter="packerEnter" @mouseleave="packerLeave">
        <div class="download-ios-left float-left">
          <a href="downloadApp.html">下载ios版 App</a>
        </div>
        <div class="download-ios-img float-right">
          <img :src="packer"/>
        </div>
      </div>
    </div>
    <div class="download-weixin-wrap">
      <div class="download-ios clear_float" @mouseenter="packerEnter1" @mouseleave="packerLeave1">
        <div class="download-ios-left float-left">
          <a href="downloadWechat.html">关注微信公众号</a>
        </div>
        <div class="download-ios-img float-right">
          <img :src="weixin"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: '',
    props: ['index'],
    data() {
      return {
        packer:require('../../assets/woodpecker.png'),
        weixin:require('../../assets/weixinPublic.png'),
        recoUsers: []
      }
    },
    methods: {
      imgEnter(index) {
        this.$refs.mask[index].className = 'user-avatar-overlay';
      },
      imgLeave(index) {
        this.$refs.mask[index].className = '';
      },
      packerEnter(){
        this.packer = require('../../assets/woodpecker_hover.png')
      },
      packerLeave(){
        this.packer = require('../../assets/woodpecker.png')
      },
      packerEnter1(){
        this.weixin = require('../../assets/weixinPublic_hover.png')
      },
      packerLeave1(){
        this.weixin = require('../../assets/weixinPublic.png')
      },

    },
    mounted() {
      var _this = this;
      axios.get('api/web_reco_users').then(function (response) {
        var array = response.data.reco_users;
        for (var i = 0; i < array.length; i++) {
          _this.recoUsers.push(array[i])
        }
      }).catch(function (err) {
        console.log(err);
      })
    }

  }
</script>

<style scoped>
  /*浮动左*/
  .float-left{
    float: left;
  }
  /*浮动右*/
  .float-right{
    float: right;
  }
  /*清除浮动必须加到父级元素上*/
  .clear_float::after{
    content: "";
    display: table;
    clear: both;
  }


  .recommend-users {
    margin-right: -218px;
    margin-top: 34%;

  }

  .side-title {
    font-size: 16px;
    font-weight: 500;
    color: #272c2f;
  }

  .users-list {
    margin-top: 8px;
  }

  .user-item {
    width: 220px;
    position: relative;
    border-bottom: 1px solid #e4e4e5;
    padding: 10px 0;
    background-color: transparent;
  }

  .recommend-users .user-name a {
    font-weight: 500;
    color: #535557;
  }

  .user-name a:hover {
    color: #999A9A;
    text-decoration: none;
  }

  .user-item .user-intro a:hover {
    color: #000000;
    text-decoration: none;
  }

  .recommend-users .user-intro {
    padding-top: 5px;
  }

  .recommend-users .user-intro a {
    font-size: 12px;
    line-height: 18px;
    color: #999a9a;
  }

  .recommend-users .user-avatar {
    position: absolute;
    top: 16px;
    right: 5px;
    font-size: 0;
  }

  .recommend-users .user-avatar-overlay {
    width: 40px;
    height: 40px;
    background-color: rgba(0, 0, 0, 0.4);
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    border-radius: 4px;
    -webkit-transition-duration: .3s;
    transition-duration: .3s;
    -webkit-transition-property: background-color;
    transition-property: background-color;
  }

  .recommend-users .user-avatar img {
    width: 40px;
    height: 40px;
    border: 1px solid #e4e4e5;
  }

  .zuo-img-rounded {
    border-radius: 4px;

  }

  .user-text-info {
    width: 146px;
  }
  .download-wrap{
    margin-top: 30px;
  }
  .download-weixin-wrap{
    margin-top: 5px;
  }
  .download-ios{
    display: inline-block;
    width: 220px;
    height: 50px;
    border: 1px solid #ececec;
    border-radius: 4px;
  }
  .download-ios:hover{
    background-color: white;
  }
  .download-ios-left{
    margin-left: 30px;
  }
  .download-ios-left a{
    width: 169px;
    height: 50px;
    line-height: 50px;
  }
  .download-ios-img{
    position: relative;
    width: 50px;
    height: 50px;
    border: 1px solid #ececec;
  }
  .download-ios-img img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate3D(-50%, -50%, 0);
    border-radius: 4px;
    width: 75%;
    height: 75%;
  }


</style>
