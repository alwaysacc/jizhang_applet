<template>
  <div id="app">
    <div class="top">
      <a>本月支出</a>
      <a style="font-size:2rem">0.00</a>
      <div class="top2">
        <span>
          <text>本月收入:</text>
          <text>0</text>
        </span>
        <span style="padding-left: 5rem;">
          <text>本月盈余:</text>
          <text>0</text>
        </span>
      </div>
    </div>
    <div class="bot">
      <button @click="addincome">记一笔</button>
      <div class="date">
        <span>
          <text>3月1日</text>
        </span>
        <span style="padding-left:9rem;">
          <text>支出:0</text>  &nbsp;&nbsp;
          <text>收入:0</text>
        </span>
      </div>
      <i-cell-group>
        <i-cell title="只显示箭头" label="2019年3月1日11:29:30" value="555.0">
          <text>666</text>
        </i-cell>
        <i-cell title="只显示箭头" label="2019年3月1日11:29:30" value="555.0">
          <text>666</text>
        </i-cell>
        <i-cell title="只显示箭头" label="2019年3月1日11:29:30" value="555.0">
          <text>666</text>
        </i-cell>
      </i-cell-group>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      motto: 'Hello miniprograme',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'
      }
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
    }
  },
  created () {
    // let app = getApp()
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
</style>
