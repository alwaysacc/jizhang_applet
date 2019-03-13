<template>
  <div class="home">
    <textarea v-model="suggest.content" placeholder="请输入你的意见和建议">
    </textarea>
    <button @click="add" type="primary">提交</button>
  </div>

</template>

<script>
export default {
  name: 'suggest',
  data () {
    return {
      suggest: {
        content: '',
        userid: ''
      }
    }
  },
  methods: {
    add () {
      let t = this
      const user = wx.getStorageSync('user')
      t.suggest.userid = user.id
      console.log(t.income)
      t.$http.post({
        url: 'suggest/add',
        data: {
          suggest: JSON.stringify(t.suggest)
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
    text-align: center;
  }
.home textarea{
  margin: 0.5rem auto;
  text-align: left;
  width: 90%;
  height: 3rem;
  background-color: white;
}
  .home button{
    width: 50%;
  }
</style>
