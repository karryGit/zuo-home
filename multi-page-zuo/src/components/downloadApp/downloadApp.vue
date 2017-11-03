<template>
  <div  id="wrap" @click="clicked">
    <img src="../../assets/download/ios.png"/>
  </div>
</template>

<script>
  export default {
    name: 'downloadApp',
    methods: {
      clicked() {
        window.location.href = 'index.html'
      }
    }
  }
</script>
<style scoped>
  @import "../../common/style/marx.min.css";

  #wrap {
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    z-index: 100;
    background-color: rgba(39, 44, 47, .9);
  }

  #wrap img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate3D(-50%, -50%, 0);
  }


</style>
