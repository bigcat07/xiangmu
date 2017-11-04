<template>
  <div>
    <div v-for="(v,i) in array" class="content">
      <div class="head">
        <div class="left">
          <a href="#">
            <img :src="v.author.avatar" alt="" class="headimg">
          </a>
          <a href="#">
            <span class="author">{{v.author.username}}</span>
          </a>
        </div>
        <div class="right">
          <span>{{v.timeAgo}}</span>
        </div>
      </div>
      <!--内容区-->
      <div class="mainContent">
        <p v-html="v.text"></p>
        <div class="img" v-if="v.attach_imgs.length>0">
          <img :src="v.attach_imgs[0]" alt="">
        </div>
      </div>
      <!--评论-->
      <div class="pl">
        <div class="revert">回复</div>
        <div class="zan">{{v.upvote_count}}</div>
        <div class="cai">{{v.downvote_count}}</div>
      </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: '',
        data() {
          return {
            array:[]
          }
        },
        mounted() {
          var _that = this
          axios.get('api/topic/575bb18e6be3ff0069503da2/hot_comments').then(
            function (res) {
              _that.array = res.data.hot_comments
            }
          )
        }
    }
</script>

<style scoped>
  .content {
    border-top: 1px solid darkgray;
    margin-top: 20px;
    width: 540px;
    background-color: rgb(245,245,245);
    padding-top: 20px;
  }
  .head {
    overflow: hidden;
  }
  .left {
    float: left;
  }
  .left>a {
    text-decoration: none;
  }
  .right {
    float: right;
    margin-top: 4px;
  }
  /*头像*/
  .headimg {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    vertical-align: middle;
  }
  .author {
    color: #A6A7A7;
    font-size: 14px;
    margin-left: 10px;
  }
  .right>span {
    font-size: 12px;
    color: #75797B;
  }
  .mainContent {
    padding: 20px 55px;
  }
  .img {
    width: 72px;
    height: 120px;
  }
  .img>img {
    width: 100%;
    height: 100%;
    object-fit:cover;
    cursor: pointer;
  }
  .pl {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    width: 150px;
    margin-left: 50px;
  }
  .revert {
    cursor: pointer;
  }
  .zan {
    width: 40px;
    padding-left: 25px;
    background: url("../../assets/zan.png") left no-repeat;
    cursor: pointer;
  }
  .cai {
    width: 40px;
    padding-left: 25px;
    background: url("../../assets/cai.png") left no-repeat;
    cursor: pointer;
  }
</style>
