<template>
  <div>
    <open-data type="userAvatarUrl"></open-data>
    <open-data type="userNickName"></open-data>
  </div>
</template>

<script>
export default {
  name: 'user',
  methods: {

  },
  onLoad: function (options) {
    wx.getSetting({
      success (res) {
        console.log(res)
        if (!res.authSetting['scope.record']) {
          wx.getUserInfo({
            scope: 'scope.userInfo',
            success () {
            // 用户已经同意小程序使用录音功能，后续调用 wx.startRecord 接口不会弹窗询问
              wx.startRecord()
            }
          })
        }
      }
    })
  }
}
</script>

<style scoped>

</style>
