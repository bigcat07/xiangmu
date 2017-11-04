<template>
  <div>
    <div class="posts" v-for="(v,i) in array">
      <!--作者-->
      <div class="author">
        <a href="#">
          <img :src="v.owner.avatar" alt="">
          {{v.owner.username}}
        </a>
        <div class="information">
          <div class="endorse">
            <img src="../../assets/georama.png" alt="" class="georame">
            <span class="applaud">{{v.likeCount}}个赞同</span>
          </div>
          <!--分享和举报-->
          <div class="share">
            <a href="#" class="shareshine">
              <img src="../../assets/share.png" alt="">
            </a>
            <a href="#" class="more">...</a>
          </div>
        </div>
      </div>
      <!--图片-->
      <div class="picture" @mouseenter="maskOver(i)" @mouseleave="maskOut(i)">
        <div class="praise"
             :style="{left:(v.haloCenterRatio.width_ratio*100)+'%',
           top:(v.haloCenterRatio.height_ratio*100)+'%'}">
              <p v-if="isApproved">赞同</p>
              <span v-if="isApproved">这个态度</span>
        </div>
        <div class="outer" :style="{left:(v.haloCenterRatio.width_ratio*100)+'%',
           top:(v.haloCenterRatio.height_ratio*100)+'%'}">

        </div>
      </div>
      <img :src="v.postImage.url" alt="" class="picture-img">
      <!--赞-->

      <!--下方描述-->
      <div class="describe">
        {{v.postDescription}}
      </div>
      <!--其他类型-->
      <div class="rest">
        <div class="ball" :style="{backgroundColor:v.sceneTag.color}"></div>
        <a href="#" class="contenttype">{{v.sceneTag.name}}</a>
        <a href="#" class="retall" v-if="v.tags.length>0">
          <span class="ball"></span>
          {{v.tags[0]}}
        </a>
        <a href="#" class="retall" v-if="v.tags.length>1">
          <span class="ball"></span>
          {{v.tags[1]}}
        </a>
      </div>
      <p class="line"></p>
      <div class="critic">
        <img src="../../assets/critic.png" alt="">
        <span>{{v.commentedCount}}条评论</span>
        <a href="#">更多评论...</a>
      </div>
      <!--评论区-->
      <div class="discuss">
        <div class="discussList" :style="{backgroundColor:color}"
             @mouseenter="over" @mouseleave="out">
          <div>
            <a href="#" class="username">{{v.comments[0].author.username}}</a>
            <span>-&nbsp;</span>
            <span class="text">{{v.comments[0].text}}</span>
          </div>
          <!--时间-->
          <div class="comment-actions">
            <span class="time">{{v.comments[0].timeAgo}}</span>
            <span class="replay">
                <a href="#" v-if="isReplay">回复</a>
                <span>
                  <a href="">
                     点亮{{v.comments[0].likeNumber}}
                     <img src="../../assets/lighten.png" alt="" class="lighten">
                  </a>
                 </span>
              </span>
          </div>
        </div>
        <div class="discussList" :style="{backgroundColor:colors}"
            @mouseenter="overs" @mouseleave="outs" v-if="v.comments.length>1">
          <div>
            <a href="#" class="username">{{v.comments[1].author.username}}</a>
            <span>-&nbsp;</span>
            <span class="text">{{v.comments[1].text}}</span>
          </div>
          <!--时间-->
          <div class="comment-actions">
            <span class="time">{{v.comments[1].timeAgo}}</span>
            <span class="replay">
                <a href="#" v-if="isReplays">回复</a>
                <span>
                  <a href="">
                     点亮{{v.comments[1].likeNumber}}
                     <img src="../../assets/lighten.png" alt="" class="lighten">
                  </a>
                 </span>
              </span>
          </div>
        </div>
      </div>
      <p class="line"></p>
      <textarea class="textarea" placeholder="写下你的评论..." @click="focus(i)"></textarea>
      <div class="cancel">
        <span class="call" @click="call(i)">取消</span>
        <span>评论</span>
      </div>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    var textareas = document.getElementsByClassName('textarea')
    var masks = document.getElementsByClassName('picture')
    var cancel = document.getElementsByClassName('cancel')
    export default {
        name: '',
        data() {
          return {
            array:[],
            color:'',
            colors:'',
            isReplay:false,
            isReplays:false,
            isApproved:false
          }
        },
        methods: {
          over:function () {
            this.color = 'rgb(245,245,245)'
            this.isReplay = true
          },
          out:function () {
            this.color = 'white'
            this.isReplay = false
          },
          overs:function () {
            this.colors = 'rgb(245,245,245)'
            this.isReplays = true
          },
          outs:function () {
            this.colors = 'white'
            this.isReplays = false
          },
          focus:function (i) {
            textareas[i].style.height = '100px'
            cancel[i].style.display = 'block'
          },
          call:function (i) {
            textareas[i].style.height = '50px'
            cancel[i].style.display = 'none'
          },
          maskOver:function (i) {
            masks[i].style.backgroundColor = 'rgba(0,0,0,0.3)'
            this.isApproved = true
          },
          maskOut:function (i) {
            masks[i].style.backgroundColor = 'rgba(255,255,255,0)'
            this.isApproved = false
          }
        },
        mounted () {
          var _that = this
          axios.get('api/web_hot_posts').then(
            function (res) {
              _that.array = res.data.posts
            }
          )
        }
    }
</script>

<style scoped>
  .posts {
    width: 540px;
    background-color: white;
    position: relative;
    margin-top: 20px;
  }
  .author {
   margin-left: 15px;
    position: relative;
    margin-top: 10px;
  }
  .author>a {
    text-decoration: none;
    color: black;
    font-size: 14px;
  }
  .author>a>img {
    display: inline-block;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    vertical-align: middle;
    margin-right: 5px;
  }
  .information {
    width: 180px;
    height: 30px;
    display: inline-block;
    position: absolute;
    right: 10px;
    top: 5px;
  }
  .georame {
    vertical-align: middle;
    margin-top: -5px;
    margin-right: 5px;
    margin-left: 10px;
  }
  /*赞同*/
  .endorse {
    display: inline-block;
    padding-top: 5px;
  }
  .share {
    display: inline-block;
  }
  .shareshine {
    position: absolute;
    top:7px;
    left: 120px;
  }
  .more {
    position: absolute;
    top: -7px;
    left: 140px;
    text-decoration: none;
    color: #B8B9B9;
    font-size: 24px;
  }
  /*图片*/
  .picture {
    margin-top: 10px;
    position: relative;
    height: 540px;
    width: 100%;
    margin-bottom: 20px;
    z-index: 5;
  }
  .picture:hover .praise{
    border: 4px solid #00DAE2;
  }
  .picture-img {
    position: absolute;
    left: 0;
    top: 50px;
  }
  /*赞*/
  .praise {
    position: absolute;
    width: 120px;
    height: 120px;
    border: 2px solid #00DAE2;
    border-radius: 50%;
    margin-top: -60px;
    margin-left: -60px;
    text-align: center;
  }
  .praise>p {
    line-height: 100px;
    font-size: 24px;
    font-weight: 600;
    color: white;
  }
  .praise>span{
    display: inline-block;
    position: absolute;
    width: 80px;
    top: 70px;
    left: 20px;
    color: white;
    font-size: 14px;
  }
  .outer {
    position: absolute;
    width: 120px;
    height: 120px;
    border: 1px solid #00DAE2;
    border-radius: 50%;
    margin-top: -60px;
    margin-left: -60px;
    animation: animate 1.2s infinite;

  }
  @keyframes animate {
    0%{
      transform:scale(1);
      opacity:1
    }
    100%{
      transform: scale(1.5);
      opacity: 0;
    }
  }
  /*下方描述*/
  .describe {
    width: 490px;
    margin: auto;
    font-size: 14px;
    color: #595C5D;
  }
  .rest {
    width: 490px;
    height: 30px;
    margin: auto;
    margin-top:20px;
  }
  .rest>div  {
    display: inline-block;
  }
  .rest>a {
    text-decoration: none;
  }
  /*球*/
  .ball {
    display: inline-block;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    vertical-align: middle;
    background-color: #A6A7A7;
  }
  .contenttype {
    text-decoration: none;
    color: #A6A7A7;
    font-size: 14px;
  }
  /*零售空间*/
  .retall {
    display: inline-block;
    margin-left: 10px;
    font-size: 14px;
    color: #ACAEAD;
  }
  .line {
    width: 490px;
    margin: auto;
    margin-top: 20px;
    margin-bottom: 20px;
    height: 1px;
    background-color: #ECECEC;
  }
  .critic {
    width: 490px;
    margin: auto;
  }
  .critic img span {
    display: inline-block;
  }
  .critic>img {
    vertical-align: middle;
    width: 18px;
    height: 18px;
  }
  .critic>span {
    font-size: 15px;
    color: #A6A7A7;
    margin-left: 10px;
    cursor: pointer;
  }
  .critic>a {
    font-size: 15px;
    color: #A6A7A7;
    margin-left: 10px;
    text-decoration: none;
  }

  .username {
    text-decoration: none;
    color: #262D2F;
    font-size: 12px;
  }
  .text {
    font-size: 12px;
    color: #595C5D;
  }
  .comment-actions {
    margin-top: 5px;
    overflow: hidden;
  }
  .time {
    font-size: 12px;
    color: #C9C9C9;
    float: left;
  }
  .replay {
    float: right;
    line-height: 10px;
  }
  .replay>a {
    margin-right: 10px;
  }
  .replay>a, .replay>span>a {
    color: #A1A2A6;
    font-size: 12px;
    text-decoration: none;
  }
  .lighten {
    width: 10px;
    height: 10px;
  }
  .discussList {
    width: 510px;
    margin: auto;
    padding: 10px;
  }
  .textarea {
    width: 490px;
    margin: auto;
    resize: none;
    outline: none;
    border:none;
    font-size: 14px;
  }
  .cancel {
    overflow: hidden;
    width: 490px;
    margin: auto;
    margin-top: 10px;
    display: none;
  }
  .cancel>span:nth-child(1) {
    float: left;
    font-size: 14px;
    color: #502D57;
    cursor: pointer;
  }
  .cancel>span:nth-child(2) {
    float: right;
    font-size: 14px;
    color: #262D2F;
    cursor: pointer;
  }

</style>
