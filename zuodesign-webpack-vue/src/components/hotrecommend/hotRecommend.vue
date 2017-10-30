<template>
    <div>
      <div id="hottags">
        <p>热门标签</p>
        <a href="" v-for="value in this.nameArr">{{value}}</a>
      </div>
    </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: '',
        data () {
          return {
            nameArr: []
          }
        },
        mounted () {
          var _that = this;
          axios.get('api/web_hot_tags').then(
            function (res) {
              for (var i = 0;i<res.data.hot_tags.length;i++) {
                _that.nameArr.push(res.data.hot_tags[i].content)
              }
              console.log(_that.nameArr)
            }
          )
        }
    }
</script>

<style scoped>
  #hottags {
    width: 250px;
  }
  #hottags>p {
    font-weight: 600;
  }
  #hottags>a {
    text-decoration: none;
    display: inline-block;
    padding: 5px 7px;
    margin-right: 7px;
    margin-bottom: 10px;
    background-color: #eaeced;
    color: rgba(135, 158, 185, 0.68);
    border-radius: 6px;
    font-size: 18px;
  }
  #hottags>a:hover {
    color: white;
    background-color: rgb(152,155,156);
  }
</style>
