<template>
  <div>
    <div class="main" v-for="(v,i) in array">
        <div class="header">
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
        <!--内容-->
        <div class="content">
          <p style="font-size: 14px">{{v.text}}</p>
        </div>
        <!--评论-->
      <div class="pl">
        <div class="revert">回复</div>
        <div class="zan">{{v.upvote_count}}</div>
        <div class="cai">{{v.downvote_count}}</div>
      </div>
      <div class="replay" v-if="v.child_nodes.length>0">
        <div class="header">
          <div class="left">
            <a href="#">
              <img :src="v.child_nodes[0].author.avatar" alt="" class="headimage">
            </a>
            <a href="#">
              <span class="author">{{v.child_nodes[0].author.username}}</span>
            </a>
          </div>
          <div class="right">
            <span>{{v.child_nodes[0].timeAgo}}</span>
          </div>
        </div>
        <div class="text" v-html="v.child_nodes[0].text">

        </div>
      </div>
    </div>
    <button id="login" type="button">登录可参与讨论</button>
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
          axios.get('api/topic/575bb18e6be3ff0069503da2/comments').then(
            function (res) {
              _that.array = res.data.comments
            }
          )
        }
    }
</script>

<style scoped>
  .main {
    width: 540px;
    padding-top: 20px;
    border-top: 1px solid darkgray;
    margin-top: 20px;
  }
  .header {
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
  .headimg {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    vertical-align: middle;
  }
  .headimage {
    width: 30px;
    height: 30px;
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
  .content {
    padding: 20px 55px;
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
  .replay {
    width: 490px;
    border-top: 1px solid darkgray;
    margin-top: 20px;
    margin-left: 50px;
  }
  .text {
    font-size: 14px;
    text-decoration: none;
    margin-top: 15px;
  }
  #login {
    width: 540px;
    height: 50px;
    background-color: #DFDFE0;
    text-align: center;
    line-height: 30px;
    margin-top: 30px;
    color: black;
    outline: none;
    background-image: url("../../assets/loginer.png");
    background-repeat: no-repeat;
    background-position-x: 190px;
    background-position-y: 15px;
    border: none;
  }



</style>
