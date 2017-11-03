<template>
  <div>
    <div id="backTop" v-show="isBack">
      <a href="#"><img src="../../assets/images/返回顶部.png"/></a>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'backTop',
    data() {
      return {
        isBack: false
      }
    },
    methods: {
      menu() {
        var _this = this;
        document.onmousewheel = function (e) {
          var e = e || window.event;
          if (e.wheelDelta > 0) {
                 _this.isBack = false;
          } else {
              _this.isBack = true;
          }
        }
      }
    },
    mounted() {
      window.addEventListener('scroll', this.menu)
    }
  }
</script>

<style scoped>
  #backTop {
    position: fixed;
    z-index: 3000;
    right: 10%;
    top: 80%;
    width: 40px;
    height: 40px;
  }

  #backTop img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate3D(-50%, -50%, 0);
    width: 100%;
    height: 100%;
    object-fit: cover;
  }


</style>
