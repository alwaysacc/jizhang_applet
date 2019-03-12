<template>
  <div id="app">
    <div class="top">
      <a>本月支出</a>
      <a style="font-size:2rem">{{zhichu}}</a>
      <div class="top2">
        <span>
          <text>本月收入:</text>
          <text>{{shouru}}</text>
        </span>
        <span style="padding-left: 5rem;">
          <text>本月盈余:</text>
          <text>{{shouru - zhichu}}</text>
        </span>
      </div>
    </div>
    <div class="bot">
      <button @click="addincome">记一笔</button>
      <div class="date">
        <span>
          <text>今日</text>
        </span>
        <span style="padding-left:9rem;">
          <text>支出:{{zhichu}}</text>  &nbsp;&nbsp;
          <text>收入:{{shouru}}</text>
        </span>
      </div>
      <i-cell-group v-if="!showdiv">
        <i-cell v-for="t in income" :key="index"  :title="t.category" :label="t.dates" :value="t.amount" @click="toDetail(t.id,t.type)"  is-link>
          <text>{{t.remarks}}</text>
        </i-cell>
      </i-cell-group>
      <div class="none" v-if="showdiv">
        <p>什么都没有呢</p>
        <button @click="addincome">记一笔</button>
      </div>
    </div>
    <i-load-more tip="已加载完毕" :loading="false" v-if="line"/>
  </div>
</template>

<script>
export default {
  data () {
    return {
      income: [],
      page: 1,
      size: 5,
      maxpage: '',
      line: false,
      showdiv: false,
      zhichu: '',
      shouru: ''
    }
  },
  components: {
  },
  methods: {
    bindViewTap () {
      const url = '../logs/main'
      if (mpvuePlatform === 'wx') {
        mpvue.switchTab({ url })
      } else {
        mpvue.navigateTo({ url })
      }
    },
    clickHandle (ev) {
      console.log('clickHandle:', ev)
      // throw {message: 'custom test'}
    },
    addincome () {
      const url = '../addincome/main'
      mpvue.navigateTo({ url })
    },
    login () {
      var t = this
      wx.login({success: function (res) {
        console.log(res)
        if (res.code) {
          t.$http.post({
            url: 'user/dologin',
            data: {
              code: res.code
            }
          }).then(res => {
            console.log('!!!')
            console.log(res.data.data)
            wx.setStorage({
              key: 'user',
              data: res.data.data
            })
          })
          // 把获取到的code通过一个request的请求发给java服务器
        }
      }
      })
    },
    getList (e) {
      var t = this
      t.$http.post({
        url: 'income/list',
        data: {
          page: t.page,
          size: t.size,
          userid: wx.getStorageSync('user').id
        }
      }).then(res => {
        console.log(res)
        if (e === 1) {
          t.income = t.income.concat(res.data.data.list.list)
        } else {
          t.income = res.data.data.list.list
        }
        if (t.income.length === 0) {
          t.showdiv = true
        } else {
          t.showdiv = false
        }
        t.maxpage = res.data.data.list.lastPage
        t.zhichu = res.data.data.income
        t.shouru = res.data.data.outlay
      })
    },
    toDetail (e1, e2) {
      const url = '../detail/main?id=' + e1 + '&&type=' + e2
      mpvue.navigateTo({ url })
    }
  },
  created () {
  },
  onLoad () {
    var t = this
    wx.getSetting({
      success (res) {
        if (res.authSetting['scope.userInfo']) {
          const res = wx.getStorageInfoSync()
          var num = res.keys.indexOf('user')
          if (num === -1) {
            t.login()
          } else {
            t.getList()
          }
          // 已经授权，可以直接调用 getUserInfo 获取头像昵称
        } else {
          const url = '../start/main'
          mpvue.navigateTo({ url })
        }
      }
    })
  },
  onReachBottom () {
    var t = this
    // 下拉触底，先判断是否有请求正在进行中
    // 以及检查当前请求页数是不是小于数据总页数，如符合条件，则发送请求
    if (!t.loading && t.page < t.maxpage) {
      console.loe(111111111111111)
      t.page = t.page + 1
      this.getList(1)
    } else {
      t.line = true
    }
  },
  onShow () {
    var t = this
    t.getList()
  }
}
</script>

<style scoped>
#app {
  padding: 0.1rem;
  margin: 0.1rem;
}
a {
  font-size: 0.3rem;
}
.top {
  padding-top: 0.7rem;
  height: 2.5rem;
  background-color: #fa7a1f;
  padding-left: 0.2rem;
}
.top2 {
  padding-top: 0.2rem;
  font-size: 0.3rem;
}
.bot {
  margin-top: 0.2rem;
  font-size: 0.3rem;
}
.bot button {
  background-color: #fa7a1f;
}
.date {
  height: 0%;
}
.date {
  height: 0.4rem;
  color: darkgray;
  padding-top: 0.3rem;
  padding-left: 0.3rem;
}
.none{
  text-align: center;
  height: 3rem;
  position: absolute;
  margin: auto;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
.none p{
  color: darkgrey;
  font-size: 0.3rem;
  padding-top: 2rem;
}
.none button{
  background-color: #fa7a1f;
  width: 3rem;
  margin-top: 0.2rem;
}
</style>
