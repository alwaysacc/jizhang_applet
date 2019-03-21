<template>
  <div class="wraper">
    <div class="container">
      <div class="section-two">
        <div class="tab">
          <a :class="currentTab=='0'?'nav active': 'nav'" data-current="0" @click="switchTab('switchTab',$event)">本日</a>
          <a :class="currentTab=='1'?'nav active': 'nav'" data-current="1" @click="switchTab('switchTab',$event)">本周</a>
          <a :class="currentTab=='2'?'nav active': 'nav'" data-current="2" @click="switchTab('switchTab',$event)">本月</a>
          <a :class="currentTab=='3'?'nav active': 'nav'" data-current="3" @click="switchTab('switchTab',$event)">本年</a>
        </div>
        <swiper class="cont" @change="switchItem('switchItem',$event)" :current="currentTab" circular="true" skip-hidden-item-layout="true">
          <swiper-item>
            <scroll-view scroll-y="true" @scrolltolower="a">
            <div class="item">
              <top :msg="msg2" :income="zhichu" :outlay="shouru"></top>
            </div>
            <clist :list="list" v-if="!showdiv"></clist>
            <div class="none" v-if="showdiv">
              <p>什么都没有呢</p>
              <button @click="addincome">记一笔</button>
            </div>
            </scroll-view>
          </swiper-item>
          <swiper-item>
            <scroll-view scroll-y="true" @scrolltolower="a">
            <div class="item">
              <top :msg="msg2" :income="zhichu" :outlay="shouru"></top>
              <clist :list="list" v-if="!showdiv"></clist>
              <div class="none" v-if="showdiv">
                <p>什么都没有呢</p>
                <button @click="addincome">记一笔</button>
              </div>
            </div>
            </scroll-view>
          </swiper-item>
          <swiper-item>
            <scroll-view scroll-y="true" @scrolltolower="a">
            <div class="item">
              <top :msg="msg3" :income="zhichu" :outlay="shouru"></top>
              <clist :list="list" v-if="!showdiv"></clist>
              <div class="none" v-if="showdiv">
                <p>什么都没有呢</p>
                <button @click="addincome">记一笔</button>
              </div>
            </div>
            </scroll-view>
          </swiper-item>
          <swiper-item>
            <scroll-view scroll-y="true" @scrolltolower="a">
            <div class="item">
              <top :msg="msg4" :income="zhichu" :outlay="shouru"></top>
              <clist :list="list" v-if="!showdiv"></clist>
              <div class="none" v-if="showdiv">
                <p>什么都没有呢</p>
                <button @click="addincome">记一笔</button>
              </div>
            </div>
            </scroll-view>
          </swiper-item>
        </swiper>
      </div>
    </div>
    <i-message id="message" />
  </div>
</template>

<script>
import clist from '@/components/clist'
import top from '@/components/top'
import {$Message} from '../../../static/iView/base/index'
export default {
  name: 'statistics',
  data () {
    return {
      msg1: '日',
      msg2: '周',
      msg3: '月',
      msg4: '年',
      currentTab: '0',
      list: [
      ],
      by: '天',
      showdiv: false,
      zhichu: '',
      shouru: '',
      page: 0,
      size: 5,
      maxpage: '',
      line: false
    }
  },
  components: {
    clist,
    top,
    $Message
  },
  methods: {
    switchTab: function (prompt, res) {
      var t = this
      // console.log(prompt,res);
      var oIndex = res.mp.currentTarget.dataset.current
      this.currentTab = oIndex
      console.log(oIndex)
      switch (oIndex) {
        case '0':
          t.by = '天'
          console.log(t.by)
          break
        case '1':
          t.by = '周'
          console.log(t.by)
          break
        case '2':
          t.by = '月'
          console.log(t.by)
          break
        case '3':
          t.by = '年'
      }
      t.getListByUserid()
    },
    switchItem: function (prompt, res) {
      // console.log(prompt,res.mp.detail.current);
      let oIndex = res.mp.detail.current
      this.currentTab = oIndex
    },
    getListByUserid (e) {
      var t = this
      t.$http.post({
        url: 'income/getListByUserid',
        data: {
          page: t.page,
          size: t.size,
          by: t.by,
          userid: wx.getStorageSync('user').id
        }
      }).then(res => {
        if (res.data.code === 200) {
          if (e === 1) {
            t.list = t.list.concat(res.data.data.list.list)
          } else {
            t.list = res.data.data.list.list
          }
          t.zhichu = res.data.data.income
          t.shouru = res.data.data.outlay
          t.maxpage = res.data.data.list.lastPage
          if (t.list.length === 0) {
            t.showdiv = true
          } else {
            t.showdiv = false
          }
        }
        console.log(res)
        console.log(222222)
      })
    },
    addincome () {
      const url = '../addincome/main'
      mpvue.navigateTo({ url })
    },
    // 上滑加载更多
    a () {
      var t = this
      // 下拉触底，先判断是否有请求正在进行中
      // 以及检查当前请求页数是不是小于数据总页数，如符合条件，则发送请求
      if (!t.loading && t.page < t.maxpage) {
        console.log(111111111111111)
        console.log(t.page)
        console.log(t.maxpage)
        t.page = t.page + 1
        this.getListByUserid(1)
      } else {
        $Message({
          content: '没有更多数据！',
          duration: 5
        })
      }
    }
  },
  created () {
  },
  onReady  () {
    console.log(3333)
    this.getListByUserid()
  }
}
</script>

<style scoped>
  .container {
    flex: 1;
  }
  /*第二功能模块*/
  .section-two {
    width: 100%;
    height: auto;
    background-color: #fff;
  }
  /*轮播图导航 */
  .tab {
    width: 100%;
    height: 1.3513513513513513rem;
    box-sizing: border-box;
    padding: 0.5405405405405406rem 0 0.5405405405405406rem;
    display: flex;
    align-items: center;
    border-bottom: 0.02702702702702703rem solid #ebebeb;
    font-size: 0.3rem;
  }
  .nav {
    text-align: center;
    flex: 1;
    font-weight: 600;
    box-sizing: border-box;
  }
  .nav:nth-of-type(odd) {
    border-left: 0.02702702702702703rem solid #ebebeb;
    border-right: 0.02702702702702703rem solid #ebebeb;
  }
  .nav.active {
    color: #16cc80;
  }
  /*轮播图内容*/
  .cont {
    width: 100%;
    height: 95%;
    display: flex;
    position: fixed;
  }
  scroll-view{
    width: 100%;
    height: 93%;/*动态高度*/
  }
  .none{
    text-align: center;
    height: 3rem;
    position: absolute;
    margin: auto;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
   }
  .none p{
    color: darkgrey;
    font-size: 0.3rem;
    padding-top: 2rem;
  }
  .none button{
    background-color: #fa7a1f;
    width: 3rem;
    margin-top: 0.2rem;
  }
</style>
