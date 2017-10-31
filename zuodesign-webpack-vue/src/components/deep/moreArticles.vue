<template>
  <div>
    <h4>更多文章</h4>
    <div id="mainContent">
      <div v-for="(v,i) in array">
        <!--图片-->
        <div class="picture">
          <a href="#">
            <img :src="v.banner" alt="">
          </a>
        </div>
        <!--描述-->
        <p class="title">
          <a href="#">{{v.title}}</a>
        </p>
        <!--下方作者和时间-->
        <div class="author">
          <p></p>
          <p></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: '',
        data () {
          return {
            array:[]
          }
        },
        mounted () {
          var _that = this
          axios.get('api/articles').then(
            function (res) {
              _that.array = res.data.articles
            }
          )
        }
    }
</script>

<style scoped>
  h4 {
    width: 100px;
    margin: auto;
    margin-top: 30px;
    margin-bottom: 10px;
    text-align: center;
    font-weight: 600;
  }
  #mainContent {
    width: 960px;
    margin: auto;
    border: 1px solid red;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
  }
  #mainContent>div {
    width: 218px;
    height: 315px;
    margin-top: 20px;
    position: relative;
  }
  /*图片*/
  .picture {
    width: 218px;
    height: 160px;
    overflow: hidden;
  }
  .picture img {
    border-radius: 6px;
  }
  /*描述*/
  .title {
    width: 180px;
    margin: auto;
    margin-top: 10px;
  }
  .title>a {
    text-decoration: none;
    color: rgb(38,45,47);
    font-size: 14px;
  }
  .author {
    position: absolute;
    width: 190px;
    bottom: 10px;
    overflow: hidden;
  }
  .author>p:nth-child(1) {
    float: left;
  }
  .author>p:nth-child(2) {
    float: right;
  }
</style>
