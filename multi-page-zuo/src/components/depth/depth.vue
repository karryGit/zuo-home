<template>
  <div>
    <header id="depth-container">
      <!--推荐阅读-->
      <div class="depth-body">
        <h3 class="read">推荐阅读</h3>
        <div class="imgWrap" v-for="(rticle,index) in rticles">
          <div class="maskTwo">
          </div>
          <img :src="rticle.banner"/>
          <div class="textWrap">
            <div class="img-one">
              {{rticle.title}}
            </div>
            <p class="text-one">{{rticle.summary}}</p>
          </div>
          <div class="hengxian"></div>
          <div class="text-footer clear_float">
            <a href="" class="kind">
              <span :style="{color:rticle.sceneTagColor}">●</span>
              <span>&nbsp;{{rticle.sceneTagName}}</span>
            </a>
            <a href="" class="dateline"><span>{{rticle.timeAgo}}</span></a>
          </div>
        </div>
      </div>
      <!--更多文章-->
      <div class="more-body">
        <h3 class="more">更多文章</h3>
        <div class="more-content" v-for="rticled in rticledArr">
          <div class="white"></div>
          <!--图片-->
          <div class="img-two">
            <img :src="rticled.banner"/>
          </div>
          <!--文本内容-->
          <div class="text-two">
            <a href="">
              <span>{{rticled.title}}</span>
            </a>
          </div>
          <!--底部时间部分-->
          <div class="footer-time-wrap clear_float">
            <div class="title-name float-left">
              <a href="">
                <span>zuo先生</span>
              </a>
            </div>
            <div class="title-time float-right">
              <a href="">
                <span>{{rticled.timeAgo}}</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </header>
  </div>

</template>
<script>
  import axios from 'axios';
  import MyBackTop from '../../components/index/backTop';
  export default {
    name: 'depth',
    data() {
      return {
        rticles: [],
        rticledArr: []
      }
    },
    mounted() {
      var _that = this;
      axios.get('api/hot_articles').then(function (response) {
        for (let i = 0; i < response.data.hot_articles.length; i++) {
          _that.rticles.push(response.data.hot_articles[i]);
        }
      });
      axios.get('api/articles').then(function (res) {
        for (let i = 0; i < res.data.articles.length; i++) {
          _that.rticledArr.push(res.data.articles[i])

        }
        console.log(_that.rticledArr)
      })
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

  .footer-time-wrap {
    z-index: 1;
    width: 190px;
    position: relative;
    left: 0;
    top: 91%;
    height: 40px;
  }

  .title-time a {
    font-size: 14px;
    text-decoration: none;
    color: #A4ABB0;
  }

  .title-name a {
    text-decoration: none;
    color: #262721;
    font-weight: 200;
  }

  .text-two {
    z-index: 2;
    font-size: 15px;
    width: 190px;
    position: absolute;
    bottom: 20%;
    text-align: left;
  }

  .text-two a {
    text-decoration: none;
    color: #3A230C;
    font-weight: 200;
  }

  #depth-container {
    background-color: #F6F6F6;
    margin-top: 60px;
    width: 100%;
    height: 150%;
  }

  .depth-body {
    width: 960px;
    margin: 30px auto;
  }
  .depth-body h3{
    padding-top: 30px;
  }

  .more-body {
    width: 960px;
    height: 1200px;
    margin: 0 auto;
    padding-bottom: 60px;
  }

  .more {
    text-align: center;
  }

  .read {
    text-align: center;
    width: 960px;
    margin-bottom: 30px;
  }

  .more-content {
    box-shadow:4px 4px 10px #b7b7b7;;
    margin-top: 10px;
    margin-left: 10px;
    border-radius: 5px;
    position: relative;
    display: inline-flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    width: 220px;
    height: 300px;
  }

  .img-two {
    object-fit: cover;
    position: absolute;
    border-radius: 5px;
    width: 100%;
    height: 100%;
  }
  .white{
    z-index: 1;
    background-color: white;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    width: 100%;
    height: 50%;
    position: absolute;
    bottom: 0;
  }

  .img-two img {
    border-radius: 6px;
    width: 100%;
    height: 100%;
  }

  .imgWrap {
    display: inline-flex;
    position: relative;
    margin-left: 10px;
    flex-direction: row;
    justify-content: space-around;
    border-radius: 5px;
    width: 300px;
    height: 450px;
  }

  .imgWrap:hover .maskTwo {
    opacity: 1;
  }

  .maskTwo {
    border-radius: 5px;
    opacity: 0;
    transition: all 1s;
    position: absolute;
    height: 100%;
    width: 100%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, .4);
    z-index: 1000;
  }

  .imgWrap img {
    border-radius: 5px;
    position: absolute;
    width: 100%;
    height: 100%;
  }

  .img-one {
    font-size: 18px;
    font-weight: 500;
    color: white;
    width: 280px;
  }

  .textWrap {
    text-align: left;
    position: absolute;
    bottom: 20%;
  }

  .text-one {
    margin-top: 20px;
    font-size: 16px;
    color: #E4D6D6;
    width: 280px;
  }

  .hengxian {
    position: absolute;
    left: 5%;
    bottom: 14%;
    width: 90%;
    height: 1px;
    background-color: #C3C5CA;
  }

  .text-footer {
    width: 90%;
    position: relative;
    top: 91%;
    height: 40px;
  }

  .kind {
    float: left;
  }

  .kind span:nth-child(2) {
    font-size: 14px;
    color: white;
  }

  .dateline {
    font-size: 14px;
    color: white;
    float: right;
  }


</style>
