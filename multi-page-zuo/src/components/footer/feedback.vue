<template>
  <div>
    <transition name="fade">
      <div class="mask" v-show="isFeedback" @click="feedbackClick">
        <!--意见反馈-->
        <div class="feedback-container">
          <div class="feedback-title">
            <h4>意见反馈</h4>
          </div>
          <div>
            <textarea class="feedbackTxte" name="feedback" placeholder="你有啥想ZUO的，快告诉我们呀~"></textarea>
          </div>
          <!--提交反馈-->
          <div class="submit-body">
            <a href="###">
              <span>提交反馈</span>
            </a>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
  export default {
    name: 'feedback',
    props:{
      isFeedback:null
    },
    data() {
      return {

      }
    },
    methods:{
      feedbackClick(){
        this.isFeedback=!this.isFeedback
        thi.$emit('feedback',false)
      }
    }
  }
</script>

<style scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s
  }

  .fade-enter, .fade-leave-to /* .fade-leave-active in below version 2.1.8 */
  {
    opacity: 0
  }

  .submit-body {
    width: 90%;
    height: 60px;
    border-radius: 5px;
    margin-bottom: 20px;
    background-color:#00DCE6 ;
    margin: 0 auto;
  }

  .submit-body a {
    text-decoration: none;
    text-align: center;
  }
  .submit-body span {
    line-height: 60px;
    padding-left: 43%;
    font-size: 19px;
    color: white;
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

  .feedback-container {
    width: 600px;
    height: 400px;
    border-radius: 5px;
    position: absolute;
    top: 100px;
    left: 50%;
    margin-left: -270px;
    background-color: white;
  }

  .feedback-title {
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    width: 100%;
    height: 80px;
    margin: -16px 0;
    background-color: black;
  }

  .feedback-title h4 {
    line-height: 80px;
    color: white;
    text-align: center;
  }

  .feedbackTxte {
    margin: 50px auto;
    outline: none;
    border: 1px solid #ececec;
    width: 80%;
    height: 160px;
    background-color: #f6f6f6;
    resize: none;
    padding: 15px;
  }
</style>
