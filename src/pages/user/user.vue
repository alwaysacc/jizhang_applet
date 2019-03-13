<template>
  <div id="home">

    <div class="top">
      <div class="touimage">
        <open-data type="userAvatarUrl" ></open-data>
      </div>
      <div>
        <open-data type="userNickName"></open-data>
      </div>
      <div class="bot">
        <ul>
          <li style="float: left;padding-left: 3rem">已记账{{day}}天</li>
          <li style="float: right;padding-right:3rem">已记账{{count}}笔</li>
        </ul>
      </div>
    </div>
    <div class="bottom">
      <ul>
        <li @click="a">导出账单<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li @click="err">定时提醒<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li @click="err">搜索账单<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li @click="err">消费报表<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li @click="suggest">反馈建议<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li @click="err">关于我<span><img class="img2" src="../../assets/you.png"/></span></li>
        <button open-type="share" type="primary">推荐给朋友</button>
      </ul>
    </div>
    <i-toast id="toast" />
  </div>

</template>

<script>
import {$Toast} from '../../../static/iView/base/index'
export default {
  name: 'user',
  data () {
    return {
      day: '',
      count: ''
    }
  },
  components: {
    $Toast
  },
  methods: {
    err () {
      $Toast({
        content: '该页面暂未编写....',
        type: 'error'
      })
    },
    a () {
      let url = '../email/main'
      wx.navigateTo({ url })
    },
    suggest () {
      let url = '../suggest/main'
      wx.navigateTo({ url })
    },
    onGotUserInfo (e) {
    },
    onShareAppMessage: function (ops) {
      if (ops.from === 'button') {
        // 来自页面内转发按钮
        console.log(ops.target)
      }
      return {
        title: '转发dom',
        path: `pages/index/index`,
        success: function (res) {
          // 转发成功
          console.log('转发成功:' + JSON.stringify(res))
          // var shareTickets = res.shareTickets
          // if (shareTickets.length == 0) {
          //   return false;
          // }
          // //可以获取群组信息
          // wx.getShareInfo({
          //   shareTicket: shareTickets[0],
          //   success: function (res) {
          //     console.log(res)
          //   }
          // })
        }
      }
    }
  },
  onShow () {
    let t = this
    t.$http.post({
      url: 'income/getCount',
      data: {
        userid: wx.getStorageSync('user').id
      }
    }).then(res => {
      t.count = res.data.data[0].count
      t.day = res.data.data[0].countday
      console.log(res.data.data[0].count)
      console.log(res.data.data[0].countday)
    })
  }
}
</script>

<style scoped>
  #home{
  width: 100%;
    text-align: center;

  }
  .top{
    background-color: white;
    height: 3rem;
  }
  .touimage {
    /* 居中 */
    margin: 0 auto;
    display: flex;
    justify-content: center;
    overflow: hidden;
    width: 1.8rem;
    height: 1.8rem;
    border-radius: 50%;
  }
.top .bot{
  text-align: left;
}
  .bot{
    font-size: 0.3rem;
  }
.bottom{
  text-align: left;
  margin-top: 0.2rem;
  font-size: 0.3rem;
}
  .bottom ul li{
    height: 1rem;
    line-height: 1rem;
    padding-left: 0.3rem;
    padding-bottom: 0.03rem;
    border-bottom: darkgrey 0.01rem solid;
    background-color: white;
  }
  .img{
    vertical-align: middle;
    height:1rem;
    width: 1rem;
    padding-right: 0.2rem;
  }
  .img2{
    vertical-align: middle;
    height:0.8rem;
    width: 0.8rem;
  }
  .bottom ul li span{
    float: right;
    padding-right: 0.1rem;
  }
  button{
    width: 50%;
    color: black;
    margin-top: 0.5rem;
    font-size: 0.3rem;
  }
</style>
