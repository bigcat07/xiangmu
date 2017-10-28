<template>
  <div>
    <NavgationBar></NavgationBar>
    <mainContent></mainContent>
  </div>

</template>

<script>
  import MyIndex from '../../components/index/Index'
  import NavgationBar from '../../components/navgationBar/navgationBar.vue'
  import mainContent from '../../components/maincontent/mainContent.vue'
  export default {
    name: 'index',
    components: {
        MyIndex,
        NavgationBar,
        mainContent
    }
  }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
</style>
