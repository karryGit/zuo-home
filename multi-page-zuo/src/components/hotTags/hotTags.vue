<template>
  <div>
    <section id="hot_container">
      <header class="side-title">热门标签</header>
      <button class="btn" v-for="hotTag in hotTags">
        <a href="#">{{hotTag.content}}</a>
      </button>
    </section>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {

    name: 'hotTags',
    data() {
      return {
        hotTags: [],
      }
    },
    methods: {
    },
    mounted() {
      var _this = this;
      axios.get('http://oynvlnf3a.bkt.clouddn.com/file/api/web_hot_tags.json').then(function (response) {
        var arr = response.data.hot_tags;
        for (var i = 0; i < arr.length; i++) {
          _this.hotTags.push(arr[i])
        }
      });
    }

  }
</script>

<style scoped>
  #hot_container {
    width: 234px;
    position: relative;
  }

  .side-title {
    font-size: 16px;
    font-weight: 500;
  }

  .btn {
    border: none;
    margin: 5px;
    padding: 8px;
    background-color: #EAECED;
  }

  .btn a {
    text-decoration: none;
    color: #999b9c;
  }

  .btn a:hover {
    color: #595a5b;;
  }

</style>
