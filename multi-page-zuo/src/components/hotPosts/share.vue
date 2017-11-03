<template>
  <div>
    <transition name="fade">
    <div v-show="pass" class="mask" @click="maskingClick">
      <div class="auth-box">
        <!--关闭-->
        <img class="close1" src="../../assets/close.png" @click="closeClick"/>
        <div class="share-inner">
          <div class="weixin-part">
            <div class="title-tip">
              扫一扫，
              <br>分享给微信好友！
            </div>
            <div class="weixin-qrcode-container">
              <div class="qrcode" title="http://zuodesign.cn/zuo/post/58a159ce128fe1006cf3cc8d">
                <img src="../../assets/images/weixinErWeiMa.png" height="140" width="140"/>
              </div>
            </div>
          </div>
          <div class="other-socials">
            <div class="title-tip1">复制链接</div>
            <div class="zuo-share-link">
              <span>http://zuodesign.cn/zuo/post/58a159ce128fe1006cf3cc8d</span>
            </div>
            <div class="other-socials-links">
              <a href="http://weibo.com/u/5854396168/home?wvr=5" title="新浪微博">
                <img src="../../assets/images/xinlang.png"/>
              </a>
              <a href="https://sns.qzone.qq.com/" title="QQ空间">
                <img src="../../assets/images/kongjian.png"/>
              </a>
              <a href="https://huaban.com/login/?dialog=1" title="花瓣网">
                <img src="../../assets/images/huaban.png"/>
              </a>
              <a href="https://www.douban.com/" title="豆瓣网">
                <img src="../../assets/images/douban.png"/>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
    </transition>
  </div>
</template>

<script>
  export default {
    name: 'share',
    data() {
      return {

      }
    },
    props: {
      pass: null
    },
    methods: {
      //蒙版点击事件
      maskingClick() {
        this.$emit("shareClicked", false);
      },
      closeClick() {
        this.$emit("shareClicked", false);
      }
    }
  }
</script>

<style scoped>
  @import '../../../node_modules/vue2-animate/dist/vue2-animate.min.css';
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active in below version 2.1.8 */
  {
    opacity: 0
  }

  .close1 {
    width: 20px;
    height: 20px;
    position: absolute;
    right: -5%;
    top: 2%;
  }

  .mask {
    opacity: 1;
    display: block;
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

  .auth-box {
    width: 600px;
    height: 270px;
    border-radius: 5px;
    background-color: white;
    position: relative;
    top: 150px;
    left: 50%;
    margin-left: -270px;
  }

  .share-inner {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    -webkit-box-pack: justify;
    -ms-flex-pack: justify;
    justify-content: space-between;
    padding: 30px;
    background-color: #fff;
    border-radius: 4px;
  }

  .weixin-part {
    padding-right: 20px;
    border-right: 1px solid #ececec;
  }

  .title-tip {
    font-size: 15px;
    color: #272c2f;
    font-weight: 500;
    line-height: 22px;
  }

  .weixin-qrcode-container {
    margin-top: 15px;
  }

  .qrcode {
    width: 140px;
    height: 140px;
  }

  .qrcode img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .other-socials {
    width: 350px;
  }

  .title-tip1 {
    margin-top: -12px;
    font-size: 15px;
    color: #272c2f;
    font-weight: 500;
    line-height: 22px;
  }

  .zuo-share-link {
    margin-top: 15px;
    margin-bottom: 30px;
    padding: 13px 10px;
    background-color: #f6f6f6;
    border-radius: 4px;
  }

  .zuo-share-link span {
    color: #a6a7a7;
    text-decoration: none;
    font-size: 16px;
    word-wrap: break-word;
    word-break: break-all;
  }

  .other-socials-links {
    margin-left: -20px;
  }

  .other-socials-links a {
    margin-left: 20px;
  }

</style>
