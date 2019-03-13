<template>
  <div class="home">
    <input v-model="email" placeholder="请输入接收的邮箱地址"/>
    <input v-model="mouth" type="number"  placeholder="请输入要导出的月份"/>
    <i-button class="button" @click="sendemail" type="primary" size="large">提交</i-button>
    <i-toast id="toast" />
  </div>
</template>

<script>
import {$Toast} from '../../../static/iView/base/index'
export default {
  name: 'email',
  data () {
    return {
      email: '',
      mouth: ''
    }
  },
  components: {
    $Toast
  },
  methods: {
    sendemail () {
      let t = this
      if (t.email === '') {
        $Toast({
          content: '邮箱不能为空',
          type: 'success'
        })
      } else if (t.mouth === '') {
        $Toast({
          content: '月份不能为空',
          type: 'success'
        })
      } else {
        t.$http.post({
          url: 'income/sendEmail',
          data: {
            userid: wx.getStorageSync('user').id,
            mouth: t.mouth,
            email: t.email
          }
        }).then(res => {
          console.log(res)
          if (res.data.code === 200) {
            $Toast({
              content: '导出成功',
              type: 'success'
            })
            setTimeout(function () {
              wx.navigateBack({
                delta: 1
              })
            }, 1000) // 延迟时间 这里是1秒
          }
        })
      }
    }
  }
}
</script>

<style scoped>
.home{
  text-align: center;
  font-size: 0.3rem;
  margin: 0.2rem;
}
  .home input{
    border-bottom: darkgrey 0.01rem solid;
    margin-top: 1rem;
  }
  .home .button{
    width: 50%;
    margin-top: 0.3rem;
  }
</style>
