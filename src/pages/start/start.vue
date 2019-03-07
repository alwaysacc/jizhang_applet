<template>
  <div class="home">
    <span>{{span}}</span>

    <button  open-type="getUserInfo" lang="zh_CN" @getuserinfo="onGotUserInfo">{{button}}</button>
    <button @click="d">123</button>
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
      if (e.mp.detail.iv) {
        const url = '../index/main'
        mpvue.navigateTo({ url })
        wx.login({
          success (res) {
            console.log(res)
            if (res.code) {
              this.$http.post({
                url: 'income/add',
                data: {
                },
                success: function (res) {
                  console.log(res)
                }
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
        url: 'income/list',
        data: {},
        success: function (res) {
          console.log(1)
          console.log(res)
        },
        fail: function (res) {
          console.log(2)
          console.log(res)
          // reject(false)
        },
        complete: function () {
          console.log(3)
        }
      })
    },
    d () {
      wx.request({
        url: 'http://localhost:8082/income/list', // 仅为示例，并非真实的接口地址
        method: 'POST',
        data: {},
        headers: {
          'content-type': 'application/x-www-form-urlencoded' // 默认值
        },
        success: function (res) {
          console.log(res)
          console.log(1)
        },
        fail: function (res) {
          console.log(res)
          // reject(false)
        },
        complete: function () {
          wx.hideLoading()
        }
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
