<template>
  <div id="background">
    <NavgationBar></NavgationBar>
    <Search></Search>
    <Foot></Foot>
  </div>
</template>

<script>
    import NavgationBar from '../../components/navgationBar/NavgationBar.vue'
    import Search from '../../components/search/Search.vue'
    import Foot from '../../components/footer/Foot.vue'
    export default {
        name: '',
        components: {
          NavgationBar,
          Search,
          Foot
        }
    }
</script>

<style scoped>
  @import "../../common/style/marx.min.css";
  #background {
    background-color: rgb(245,245,245);
  }
</style>
