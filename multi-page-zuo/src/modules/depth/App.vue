<template>
  <div>
    <MyNav></MyNav>
    <MyDepth></MyDepth>
    <MyBackTop></MyBackTop>
  </div>
</template>
<script>
  import MyNav from '../../components/nav/Nav';
  import MyDepth from '../../components/depth/depth';
  import MyBackTop from '../../components/index/backTop';
  export default {
    name: 'depth',
    components: {
      MyDepth,
      MyNav,
      MyBackTop
    }
  }
</script>
<style scoped>

</style>
