<template>
  <div class="home">
    <span>{{span}}</span>

    <button  open-type="getUserInfo" lang="zh_CN" @getuserinfo="onGotUserInfo">{{button}}</button>
    <button @click="w">123</button>
  </div>
</template>

<script>
export default {
  name: 'start',
  data () {
    return {
      span: '欢迎使用记账小程序',
      button: '开始使用'
    }
  },
  methods: {
    onGotUserInfo: function (e) {
      var t = this
      console.log(e)
      if (e.mp.detail.iv) {
        wx.login({
          success: function (res) {
            console.log(res)
            if (res.code) {
              t.$http.post({
                url: 'user/login',
                data: {
                  code: res.code,
                  rawData: e.mp.detail.rawData,
                  signature: e.mp.detail.signature,
                  encrypteData: e.mp.detail.encryptedData,
                  iv: e.mp.detail.iv
                }
              }).then(res => {
                console.log('!!!')
                console.log(res)
                const url = '../index/main'
                mpvue.switchTab({ url })
              })
              // 把获取到的code通过一个request的请求发给java服务器
            }
          }
        })
        // 用户取消授权
      } else {
      }
    },
    w () {
      this.$http.post({
        url: 'user/a',
        data: {
          code: '123',
          a: 'asd'
        }
      }).then(res => {
        console.log(res)
      })
    }
  }
}
</script>

<style scoped>
.home{
  margin-top: 1rem;
  text-align: center;
}
  span{

    font-size: 0.7rem;

  }
  button{
    margin-top: 2rem;
    width: 3rem;
    background-color: darkcyan;
  }
</style>
