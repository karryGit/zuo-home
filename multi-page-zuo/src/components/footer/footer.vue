<template>
  <div>
    <footer class="zuo-footer">
      <div class="footer-inner">
        <div class="footer-actions">
          <a class="scan-wechat-account-link" href="downloadWechat.html">关注公众号</a>
          <a href="www.baidu.com" target="_blank">
            关于<strong>ZUO</strong>
          </a>
          <a class="feedback-link" @click="discloseClick">反馈吐槽</a>
        </div>
        <div class="zuo-law-rights">
          <span class="company">上海设慧网络科技有限公司2016版权所有</span>
          <span class="icp-num">沪ICP备15013372号</span>
        </div>
      </div>
    </footer>
    <Myfeedback :isFeedback="isSubmitMask" @subnitMask="discloseClick"></Myfeedback>
  </div>
</template>

<script>
  import Myfeedback from '../../components/footer/feedback';

  export default {
    name: 'footer',
    data() {
      return {
        isSubmitMask: false
      }
    },
    methods: {
      discloseClick(value) {
        this.isSubmitMask = value;
      }
    },
    components: {
      Myfeedback
    }
  }
</script>

<style scoped>
  .zuo-footer {
    border: none;
    background-color: #eaeaea;
  }

  .footer-inner {
    max-width: 420px;
    margin: 0 auto;
    padding-top: 8px;
    padding-bottom: 18px;
    text-align: center;
  }

  .footer-actions a:hover {
    color: black;
  }

  .footer-actions a {
    text-decoration: none;
    font-size: 13px;
    color: #999a9a;
    margin: 0 10px;
  }

  .zuo-law-rights {
    font-size: 13px;
    color: #b8b9b9;
    margin-top: 10px;
  }

  .zuo-law-rights .company {
    padding-right: 15px;
  }

</style>
