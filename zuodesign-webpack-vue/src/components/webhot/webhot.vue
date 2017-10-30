<template>
  <div>
    <div id="nav">
      <div id="title">
        <img src="../../assets/soduku.png" alt="">
        <span>全部</span>
      </div>
      <div id="project">
        <div id="project-good">
          <a href="" @click="good()">
            <img :src="goodSrc" alt="">
            <span class="text">好设计</span>
          </a>
        </div>
        <div id="project-bad">
          <a href="" @click="bad()">
            <img :src="badSrc" alt="">
            <span class="text">坏设计</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    import projectGood from '../../assets/check-box.png'
    import projectBad from '../../assets/check-box1.png'
    import projectNone from '../../assets/check-box_click.png'
    export default {
        name: '',
        data () {
          return {
            goodSrc:projectGood,
            badSrc:projectBad
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
  }
  #title>span {
    position: absolute;
    height: 20px;
    display: inline-block;
    left: 23px;
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
</style>
