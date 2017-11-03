<template>
  <div id="all">
    <MyNav></MyNav>
    <my-index></my-index>
    <div id="wrap" class="clear_float">
      <MyHeader id="left"></MyHeader>
      <MyHotTags id="right"></MyHotTags>
      <MyAttention class="float-right"></MyAttention>
      <MyHotPosts class="float-left"></MyHotPosts>
      <MyBackTop></MyBackTop>
    </div>
    <!--底部-->
    <MyFooter></MyFooter>
  </div>
</template>
<script>
  import MyIndex from '../../components/index/Index';
  import MyNav from '../../components/nav/Nav';
  import MyHeader from '../../components/header/header';
  import MyHotTags from '../../components/hotTags/hotTags';
  import MyAttention from '../../components/Attention/Attention';
  import MyHotPosts from '../../components/hotPosts/hotPosts';
  import MyBackTop from '../../components/index/backTop';
  import MyFooter from '../../components/footer/footer';
  export default {
    name: 'index',
    components: {
      MyIndex,
      MyNav,
      MyHeader,
      MyHotTags,
      MyAttention,
      MyHotPosts,
      MyBackTop,
      MyFooter
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

  #all {
    width: 100%;
    background-color: rgb(246, 246, 246);
  }

  #wrap {
    width: 1200px;
    margin: 0 auto;
  }

  #right {
    margin-top: 4.6%;
    margin-right: 15%;
    float: right;
  }

  #left {
    float: left;
  }

  .clear_float::after {
    content: "";
    display: table;
    clear: both;
  }


</style>
