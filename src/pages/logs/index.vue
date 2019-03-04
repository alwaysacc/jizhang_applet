<template>
  <div>
    <div class="navbar">
      <block v-for="(item,index) in tabs" :key="index">
        <div :id="index" :class="{'navbar_item_on':activeIndex == index}" class="navbar_item" @click="tabClick">
          <div class="navbar_title">{{item.name}}</div>
        </div>
      </block>
      <div class="navbar_slider" :class="navbarSliderClass"></div>
    </div>
    <div>
      <div :hidden="activeIndex != 0">选项一的内容</div>
      <div :hidden="activeIndex != 1">选项二的内容</div>
      <div :hidden="activeIndex != 2">选项三的内容</div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tabs: [
        {
          name: '选项卡1',
          type: '1',
          checked: true
        },
        {
          name: '选项卡2',
          type: '2',
          checked: true
        },
        {
          name: '选项卡3',
          type: '3',
          checked: true
        }
      ],
      activeIndex: 0
    }
  },
  computed: {
    navbarSliderClass () {
      if (this.activeIndex === 0) {
        return 'navbar_slider_0'
      }
      if (this.activeIndex === 1) {
        return 'navbar_slider_1'
      }
      if (this.activeIndex === 2) {
        return 'navbar_slider_2'
      }
    }
  },
  methods: {
    tabClick (e) {
      console.log(e)
      this.activeIndex = e.currentTarget.id
    }
  }
}
</script>

<style scoped>
  .content {
    box-sizing: border-box;
    height: 100%;
    padding-top: 50px;
    /* overflow: auto; */
    -webkit-overflow-scrolling: touch;
  }

  .swiper-item {
    height: 100%;
    text-align: center;
  }

  .navbar {
    display: -webkit-box;
    display: -webkit-flex;
    display: flex;
    position: fixed;
    z-index: 500;
    top: 0;
    height: 50px;
    width: 100%;
    background-color: #298de5;
    border-bottom: 1px solid #ccc;
  }

  .navbar_item {
    position: relative;
    display: block;
    -webkit-box-flex: 1;
    -webkit-flex: 1;
    flex: 1;
    padding: 13px 0;
    text-align: center;
    font-size: 0;
  }

  .navbar_item .navbar_item_on {
    color: white;
  }

  .navbar_title {
    color: white;
    font-weight: 500;
    display: inline-block;
    font-size: 15px;
    max-width: 8em;
    width: auto;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    word-wrap: normal;
  }

  .navbar_slider {
    position: absolute;
    content: " ";
    left: 0;
    bottom: 0;
    width: 6em;
    height: 3px;
    background-color: white;
    -webkit-transition: -webkit-transform 0.1s;
    transition: -webkit-transform 0.1s;
    transition: transform 0.1s;
    transition: transform 0.1s, -webkit-transform 0.1s;
  }

  .navbar_slider_0 {
    left: 29px;
    transform: translateX(0);
  }

  .navbar_slider_1 {
    left: 29px;
    transform: translateX(250px);
  }

  .navbar_slider_2 {
    left: 29px;
    transform: translateX(500px);
  }
  .controls {
    display: -webkit-box;
    display: -webkit-flex;
    display: flex;
    position: fixed;
    z-index: 8888;
    top: 80px;
    height: 50px;
    width: 100%;
    background-color: #298de5;
  }
  .userinfo {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .userinfo-avatar {
    width: 128px;
    height: 128px;
    margin: 20px;
    border-radius: 50%;
  }

  .userinfo-nickname {
    color: #aaa;
  }

  .usermotto {
    margin-top: 150px;
  }

  .form-control {
    display: block;
    padding: 0 12px;
    margin-bottom: 5px;
    border: 1px solid #ccc;
  }
  .all{
    width:7.5rem;
    height:1rem;
    background-color:blue;
  }
  .all:after{
    display:block;
    content:'';
    clear:both;
  }
  .left{
    float:left;
    width:3rem;
    height:1rem;
    background-color:red;
  }

  .right{
    float:left;
    width:4.5rem;
    height:1rem;
    background-color:green;
  }
</style>
