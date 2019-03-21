<template>
  <div id="home">
    <i-row class="top">
      <i-col span="16" i-class="col-class"><i-input v-model="q" placeholder="请输入关键字" maxlength="20" @change="setQ"/></i-col>
      <i-col span="8" i-class="col-class"><i-button @click="search" type="primary">搜索</i-button></i-col>
    </i-row>
    <div class="bottom">
      <clist :list="list"></clist>
      <i-page v-if="showdiv" :current="page" :total="maxPage" simple @change="nextPage">
        <view slot="prev">上一页</view>
        <view slot="next">下一页</view>
      </i-page>
    </div>
  </div>
</template>

<script>
import clist from '@/components/clist'
export default {
  name: 'search',
  data () {
    return {
      q: '',
      list: '',
      showdiv: false,
      page: 0,
      size: 5,
      maxPage: ''
    }
  },
  components: {
    clist
  },
  methods: {
    setQ (e) {
      this.q = e.mp.detail.detail.value
      console.log(e)
    },
    search () {
      let t = this
      t.$http.post({
        url: 'income/select',
        data: {
          page: t.page,
          size: t.size,
          q: t.q,
          userid: wx.getStorageSync('user').id
        }
      }).then(res => {
        if (res.data.code === 200) {
          t.maxPage = Math.floor(res.data.data.total / 5)
          t.list = res.data.data.data
          t.showdiv = true
          console.log(123)
        }
        console.log(res)
        console.log(wx.getStorageSync('user').id)
      })
    },
    nextPage (e) {
      let t = this
      console.log(e)
      const type = e.target.type
      if (type === 'next') {
        t.page = t.page + 1
        t.search()
      } else if (type === 'prev') {
        t.page = t.page - 1
        t.search()
      }
    }
  }
}
</script>

<style scoped>
  #home{
    margin: 0.1rem;
    background-color: white;
  }
.top{
  height: 0.8rem;
  line-height: 0.8rem;
}
  .bottom{
    height: auto;
    background-color: white;
  }
</style>
