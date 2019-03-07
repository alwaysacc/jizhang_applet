<template>
  <div>
    <button @click="w">123</button>
    <button  open-type="getUserInfo" lang="zh_CN" @getuserinfo="onGotUserInfo">获取用户信息</button>

  </div>
</template>

<script>
export default {
  name: 'start',
  methods: {
    onGotUserInfo: function (e) {
      console.log(e)
      wx.login({
        success (res) {
          console.log(res)
          if (res.code) {
            // 把获取到的code通过一个request的请求发给java服务器

          }
        }
      })
    },
    w () {
      wx.login({
        success (res) {
          console.log(res)
          if (res.code) {
            // 把获取到的code通过一个request的请求发给java服务器

          }
        }
      })
    }
  }
}
</script>

<style scoped>

</style>
