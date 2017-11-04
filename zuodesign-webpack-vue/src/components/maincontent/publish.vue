<template>
  <div>
    <div id="content">
      <button type="button">发表你的观点...</button>
      <p id="initiator">发起人</p>
      <div class="initiator">
        <div class="header">
          <a href="">
            <img :src="initiator.avatar" alt="">
          </a>
        </div>
        <div class="maincontent">
          <div>
            <div>
              <a href="">{{initiator.nickname}}</a>
            </div>
            <div class="text">
              {{initiator.starter_intro}}
            </div>
          </div>
        </div>
      </div>
      <p>嘉宾</p>
      <div>
        <div v-for="(v,i) in array" class="out">
          <div class="header">
            <a href="#">
              <img :src="v.avatar" alt="">
            </a>
          </div>
          <div class="information">
            <div>
              <div>
                <a href="">{{v.username}}</a>
              </div>
              <div class="text">
                {{v.inviter_intro}}
              </div>
            </div>
          </div>
        </div>
      </div>
      <div>
        <p>分享这个话题</p>
        <a href="#">
          <img src="" alt="">
        </a>
        <a href="#">
          <img src="" alt="">
        </a>
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
            array:[],
            initiator:{}
          }
        },
        mounted () {
          var _that = this
          axios.get('api/topic/575bb18e6be3ff0069503da2').then(
            function (res) {
              _that.array = res.data.topic.inviters
              _that.initiator = res.data.topic.starter
            }
          )
        }
    }
</script>

<style scoped>
  #content {
    width: 240px;
  }
  button {
    outline: none;
    width: 240px;
    font-size: 14px;
    color: white;
    text-align: center;
    padding: 8px 0;
    background-color: #00DAE0;
  }
  #initiator {
    font-size: 14px;
    margin-top: 15px;
  }
  .initiator {
    position: relative;
    width: 240px;
    border-bottom: 1px solid darkgrey;
    padding-bottom: 15px;
    overflow: hidden;
  }
  .initiator>div {
    display: inline-block;
  }
  .header {
    width: 40px;
    height: 40px;
    border-radius: 4px;
  }
  .header img {
    width: 100%;
    height: 100%;
    border-radius: 4px;
    vertical-align: bottom;
  }
  .maincontent {
    /*height: 40px;*/
    margin-left: 7px;
  }
  #maincontent a {
    text-decoration: none;
    color: black;
  }
  .text {
    color: #ABACAC;
    font-size: 12px;
    word-wrap:break-word;
    width: 158px;
  }
  #content>p:nth-child(4) {
    margin-top: 10px;
    font-size: 14px;
  }
  .information {
    margin-left: 7px;
  }
  .information a {
    text-decoration: none;
  }
  .out {
    margin-bottom: 15px;
    color: black;
    border-bottom: 1px solid darkgray;
    padding-bottom: 15px;
  }
  .out>div {
    display: inline-block;
  }
</style>
