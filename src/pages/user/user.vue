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
          <li style="float: left;padding-left: 3rem">已记账0天</li>
          <li style="float: right;padding-right:3rem">已记账0笔</li>
        </ul>
      </div>
    </div>
    <div class="bottom">
      <ul>
        <li>我的账单<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li>定时提醒<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li>搜索账单<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li>消费报表<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li>反馈建议<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li>关于我<span><img class="img2" src="../../assets/you.png"/></span></li>
        <li @click="onGotUserInfo">推荐给朋友<span><img class="img2" src="../../assets/you.png"/></span></li>
      </ul>
    </div>
  </div>

</template>

<script>
export default {
  name: 'user',
  methods: {
    onGotUserInfo (e) {
      this.$http.post({
        url: 'income/list',
        data: {},
        success: function (res) {
          console.log(res)
        }
      })
    }
  },
  onLoad: function (options) {
    wx.getSetting({
      success (res) {
        console.log(res)
        if (!res.authSetting['scope.record']) {
          /* wx.getUserInfo({
            scope: 'scope.userInfo',
            success () {
            // 用户已经同意小程序使用录音功能，后续调用 wx.startRecord 接口不会弹窗询问
              wx.startRecord()
            }
          }) */
        }
      }
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
.bottom{
  text-align: left;
  margin-top: 0.2rem;
  font-size: 0.38rem;
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
</style>
