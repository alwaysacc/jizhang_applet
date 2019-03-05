<template>
  <div id="home">
    <div class="top">
      <h1>金额：666.00</h1>
    </div>
    <div class="bot">
      <i-cell-group>
        <i-cell title="类型" value="555.0">
        </i-cell>
        <i-cell title="地点" value="555.0">
        </i-cell>
        <i-cell title="备注" value="555.0">
        </i-cell>
        <i-cell title="账户" value="555.0">
        </i-cell>
        <i-cell title="时间" value="555.0">
        </i-cell>
        <i-cell title="创建时间" value="555.0">
        </i-cell>
      </i-cell-group>
    </div>
    <div class="but">
      <button @click=""   class="btn">删除</button>
      <button @click=""   class="btn">修改</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'detial',
  data () {
    return {
    }
  },
  components: {
  },
  methods: {
  },
  onLoad: function (options) {
    wx.setNavigationBarTitle({
      title: '修改后的导航栏标题',
      success: function (res) {
        // success
      }
    })
  }
}
</script>

<style scoped>
#home{
  margin: 0rem;
  padding: 0rem;
  text-align: center;
}
  .top{
    height: 2rem;
    line-height: 2rem;
    background-color: white;
  }
  .bot{
    padding-top: 0.2rem;
    text-align: left;
    font-size: 1rem;
  }
  .but{
    position: fixed;
    bottom: 0;
    width: 100%;
  }
  .btn{
    color: white;
    margin-left: 0.5rem;
    float: left;
    width: 3rem;
    background-color: #2D8CF0;
  }
</style>
