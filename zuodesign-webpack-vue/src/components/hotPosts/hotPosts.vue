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
            <span>{{v.likeCount}}个赞同</span>
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
      <div class="picture">
        <img :src="v.postImage.url" alt="">
      </div>
      <!--下方描述-->
      <div class="describe">
        {{v.postDescription}}
      </div>
      <!--其他类型-->
      <div class="rest">
        <div class="ball" :style="{backgroundColor:v.sceneTag.color}"></div>
        <a href="#" class="contenttype">{{v.sceneTag.name}}</a>
        <div class="ball" ></div>
        <a href="#">{{v.tags[0]}}</a>
        <a href="#"></a>
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
  }
  .share {
    display: inline-block;
  }
  .shareshine {
    position: absolute;
    top:3px;
    left: 120px;
  }
  .more {
    position: absolute;
    top: -10px;
    left: 140px;
    text-decoration: none;
    color: #B8B9B9;
    font-size: 24px;
  }
  /*图片*/
  .picture {
    margin-top: 10px;
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
    border: 1px solid red;
    margin: auto;
    margin-top:20px;
  }
  .rest>div  {
    display: inline-block;
  }
  /*球*/
  .ball {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    vertical-align: middle;
  }
  .contenttype {
    text-decoration: none;
    color: #A6A7A7;
    font-size: 14px;
  }

</style>
