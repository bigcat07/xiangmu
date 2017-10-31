<template>
  <div>
    <div id="nav">
      <div id="title">
        <img src="../../assets/soduku.png" alt="">
        <span>全部</span>
      </div>
      <div id="project">
        <div id="project-good" @click.prevent.stop="good">
          <a href="#">
            <img :src="goodSrc" alt="">
            <span class="text">好设计</span>
          </a>
        </div>
        <div id="project-bad" @click.prevent.stop="bad">
          <a href="#">
            <img :src="badSrc" alt="">
            <span class="text">坏设计</span>
          </a>
        </div>
      </div>
    </div>
    <!--下拉列表-->
    <div id="downlist" v-show="isShow">
      <div id="up"></div>
      <ul id="list">
          <li id="all" @mouseenter="bgColor" @mouseleave="outbgColor">
            <img :src="box" alt="">
            全部
          </li>
          <li v-for="(value,index) in typeArr"
              @mouseenter="over(index)" class="texttyple" @mouseleave="out(index)">
            <span :style="{'backgroundColor':value.color}">&nbsp&nbsp</span>
            {{value.type}}
          </li>
      </ul>
    </div>
  </div>
</template>

<script>
    import projectGood from '../../assets/check-box.png'
    import projectBad from '../../assets/check-box1.png'
    import projectNone from '../../assets/check-box_click.png'
    import soduku from '../../assets/soduku.png'
    var text = document.getElementsByClassName('texttyple')
    export default {
        name: '',
        data () {
          return {
            goodSrc:projectGood,
            badSrc:projectBad,
            box:soduku,
            isShow:true,
            isbgcolor:false,
            typeArr:[
              {color:'red',type:'日用'},
              {color:'yellow',type:'公共'},
              {color:'blue',type:'关爱'},
              {color:'black',type:'家居'},
              {color:'pink',type:'时尚'},
              {color:'orange',type:'美食'},
              {color:'purple',type:'数码'},
              {color:'red',type:'视觉'},
              {color:'yellow',type:'空间'}
            ]
          }
        },
        methods: {
          good:function () {
            if (this.goodSrc == projectGood) {
              this.goodSrc = projectNone
            }else {
              this.goodSrc = projectGood
            }
          },
          bad:function () {
            if (this.badSrc == projectBad) {
              this.badSrc = projectNone
            }else {
              this.badSrc = projectBad
            }
          },
          over:function (i) {
            text[i].style.backgroundColor = 'rgb(245,245,245)'
          },
          out:function (i) {
            text[i].style.backgroundColor = 'rgb(255,255,255)'
          },
          bgColor:function (ev) {
            ev.target.style.backgroundColor = 'rgb(245,245,245)'
          },
          outbgColor:function (ev) {
            ev.target.style.backgroundColor = 'rgb(255,255,255)'
          }
        }
    }
</script>

<style scoped>
  #nav {
    overflow: hidden;
  }
  #title {
    font-size: 14px;
    width: 70px;
    background: url("../../assets/down.png") 53px 4px no-repeat;
    cursor: pointer;
    position: relative;
    padding: 5px;
    float: left;
    margin-left: 15px;
  }
  #title>span {
    position: absolute;
    height: 20px;
    display: inline-block;
    left: 21px;
    top: 4px;
  }
  #project {
    float: right;
  }
  #project>div {
    display: inline-block;
  }
  #project>div>a>img {
    display: inline-block;
    width: 15px;
    height: 15px;
    border-radius: 4px;
    vertical-align: middle;
  }
  #project>div>a{
    text-decoration: none;
  }
  .text {
    display: inline-block;
    margin-left: 7px;
    font-size: 12px;
    color: rgb(158,158,151);
  }
  #project-bad {
    margin-left: 10px;
  }
  #downlist {
    position: relative;
    width: 120px;
    height: 500px;
    margin-top: -5px;
  }
  #up {
    position: absolute;
    width: 0;
    height: 0;
    border-left: 7px solid transparent;
    border-right: 7px solid transparent;
    border-bottom: 11px solid red;
    left: 42px;
  }
  /*全部*/
  #all>img {
    display: inline-block;
    vertical-align: middle;
    margin-top: -4px;
  }
  #list {
    position: absolute;
    width: 100px;
    border: 1px solid darkgray;
    top: 11px;
    border-radius: 4px;
  }
  #list>li {
    width: 80px;
    padding: 7px 12px;
    list-style: none;
    margin-left: -30px;
    text-align: center;
    border-radius: 6px;
    margin-top: 10px;
    cursor: pointer;
    color: #a6a7ad;
    /*background-color: rgb(245,245,245);*/
  }
  #list>li>span {
    display: inline-block;
    height: 8px;
    height: 8px;
    border-radius: 50%;
    vertical-align: middle;
    margin-top: -5px;
    margin-right: 4px;
  }
</style>
