<template>
  <div>
    <header id="header-container">
      <!--话题部分-->
      <div id="topic_container">
        <!--图片-->
        <div class="topic-body">
          <div class="topic-wrap">
            <img :src="imgSrc" alt="">
            <div class="topic-mask"></div>
          </div>
          <div class="tip-title"> 话题 </div>
          <div class="tip-divider"></div>
          <div class="topic-title">
            <span>{{topicTitle}}</span>
            <img src="../../assets/xiangyou.png" alt="">
          </div>
          <div class="topic-counts">
            <span>{{collectCount}}人收藏</span>
            <span>&nbsp;|&nbsp;</span>
            <span>{{commenCount}}个讨论</span>
          </div>
        </div>
        <!--评论-->
        <div class="topic-comments-carousel">
          <div id="carousel-body">
            <div class="carousel-body-inner" v-for="comment in comments">
              <a href="" class="carousel-link">{{comment.author.username}}</a>
              <span>:</span>
              <span class="carousel-content" v-html="comment.text">
                      <a href="" target="_blank" class="add"></a>
                    </span>
            </div>
          </div>
        </div>
      </div>

    </header>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: '',
    data() {
      return {
        imgSrc: '',
        topicTitle: '',
        collectCount: '',
        commenCount: '',
        comments: [],
      }
    },
    mounted() {
      var _that = this;
      axios.get('api/topics').then(function (response) {
        _that.imgSrc = response.data.topic.cover;
        _that.topicTitle = response.data.topic.title;
        _that.collectCount = response.data.topic.collect_count;
        _that.commenCount = response.data.topic.comment_count;
        var arr = response.data.topic.comments;
        for (var i = 0; i < arr.length; i++) {
          _that.comments.push(arr[i])
        }
      }).catch(function (err) {
        console.log(err)
      })
    },
    created() {
      setInterval(async () => {
        let first = this.comments.splice(0, 1);
        this.comments.push(...first)
      },20000)
    }
  }
</script>
<style scoped>


  #topic_container {
    width: 50%;
    margin: 56px auto;
  }

  .topic-body {
    position: relative;
    min-height: 167px;
    width: 100%;
  }

  .topic-wrap {
    width: 600px;
    height: 200px;
    position: relative;
  }

  .topic-wrap img {
    border-top-right-radius: 5px;
    border-top-left-radius: 5px;
    width: 100%;
    height: 100%;
  }

  .topic-mask {
    border-radius: 5px;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.3);
  }

  .tip-title {
    position: absolute;
    left: 3%;
    top: 10%;
    color: white;
  }

  .tip-divider {
    position: absolute;
    left: 3.5%;
    top: 18%;
    width: 20px;
    height: 5px;
    border-radius: 6px;
    background-color: #F8D440;
    margin-top: 10px;
  }

  .topic-title {
    font-size: 28px;
    color: white;
    position: absolute;
    left: 3.5%;
    top: 38%;
  }

  .topic-title img {
    position: absolute;
    left: 107%;
    top: 12%;
  }

  .topic-counts {
    position: absolute;
    left: 3.5%;
    top: 70%;
  }

  .topic-counts span {
    color: rgb(188, 179, 165);
  }

  .topic-comments-carousel {
    width: 600px;
    height: 80px;
    background-color: white;
    border-bottom-right-radius: 5px;
    border-bottom-left-radius: 5px;
  }
  #carousel-body {
    overflow: hidden;
    font-size: 14px;
    width: 90%;
    height: 55px;
    margin: 0 auto;
  }
  .carousel-body-inner {
    line-height: 42px;
  }

  .carousel-link {
    color: black;
  }

  .carousel-content {
    width: 500px;
    height: 60px;
    word-wrap: break-word;
    word-break: break-all;
    color: #999a9a;
    overflow: hidden;
  }

</style>
