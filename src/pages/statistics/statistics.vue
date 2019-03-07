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
            <div class="item">
              <top :msg="msg1"></top>
              <clist :list="today"></clist>
            </div>
          </swiper-item>
          <swiper-item>
            <div class="item">
              <top :msg="msg2"></top>
              <clist :list="today"></clist>
            </div>
          </swiper-item>
          <swiper-item>
            <div class="item">
              <top :msg="msg3"></top>
              <clist :list="today"></clist>
            </div>
          </swiper-item>
          <swiper-item>
            <div class="item">
              <top :msg="msg4"></top>
              <clist :list="today"></clist>
            </div>
          </swiper-item>
        </swiper>
      </div>
    </div>
  </div>
</template>

<script>
import clist from '@/components/clist'
import top from '@/components/top'
export default {
  name: 'statistics',
  data () {
    return {
      msg1: '日',
      msg2: '周',
      msg3: '月',
      msg4: '年',
      currentTab: '0',
      today: [
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        },
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        },
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        },
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        },
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        },
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        },
        {
          category: '123',
          date: '2019年3月1日11:29:30',
          amount: '120',
          remarks: '666'
        }
      ]
    }
  },
  components: {
    clist,
    top
  },
  methods: {
    switchTab: function (prompt, res) {
      // console.log(prompt,res);
      let oIndex = res.mp.currentTarget.dataset.current
      this.currentTab = oIndex
    },
    switchItem: function (prompt, res) {
      // console.log(prompt,res.mp.detail.current);
      let oIndex = res.mp.detail.current
      this.currentTab = oIndex
    }
  },
  created () {
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
    overflow: hidden;
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
    position: absolute;
    left: 0px;
    width: 100%;
    height: 10rem;
    font-size: 0.7567567567567568rem;

  }
  .cont swiper-item {

  }
  .cont ::-webkit-scrollbar {
    width: 0;
    height: 0;
    color: transparent;
  }
</style>
