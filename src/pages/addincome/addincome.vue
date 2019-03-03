<!-- 添加支出或收入页面 -->
<template>
  <div id="home">
    <i-tabs :current="current" color="#f759ab" @change="handleChangeScroll">
      <i-tab class="itab" key="tab1" title="支出">
      </i-tab>
      <i-tab class="itab" key="tab2" title="收入">
      </i-tab>
      <i-tab class="itab" key="tab3" title="转账">
      </i-tab>
    </i-tabs>
    <div class="center">
      <div v-if="tab1" class="tab1">
        <input type="number" v-model="value"  class="input"/>
        <i-grid>
          <i-grid-item>一日三餐</i-grid-item>
          <i-grid-item>交通出行</i-grid-item>
          <i-grid-item>其他</i-grid-item>
        </i-grid>
        <i-input value="lue3" type="textarea" title="备注：" placeholder="请输入详细地址(最多50字)" maxlength="50" />
        <i-input value="alue4" title="地址："  />
        <picker mode="date"
                :value="startDate"
                :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="startDate" title="时间："  />
          </div>
        </picker>
        <div class='keyboard' @click.stop='_handleKeyPress'>
          <div class='key-row'>
            <div class='key-cell' data-num='7'>7</div>
            <div class='key-cell' data-num='8'>8</div>
            <div class='key-cell' data-num='9'>9</div>
            <div class='key-cell' data-num='D'>C</div>
          </div>
          <div class='key-row'>
            <div class='key-cell' data-num='4'>4</div>
            <div class='key-cell' data-num='5'>5</div>
            <div class='key-cell' data-num='6'>6</div>
            <div class='key-cell' data-num='C'>清空</div>
          </div>
          <div class='key-row'>
            <div class='key-cell' data-num='1'>1</div>
            <div class='key-cell' data-num='2'>2</div>
            <div class='key-cell' data-num='3'>3</div>
            <div class='key-cell' data-num='-1'></div>
          </div>
          <div class='key-row'>
            <div class='key-cell disabled' data-num='-1'></div>
            <div class='key-cell' data-num='.'>.</div>
            <div class='key-cell' data-num='0'>0</div>
            <div class='key-cell' data-num='-1'></div>
          </div>
          <div class='key-confirm' data-num='S'>确认</div>
        </div>
      </div>
      <div v-if="tab2">2</div>
      <div v-if="tab3">3</div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      current: 'tab1',
      tab1: true,
      tab2: '',
      tab3: '',
      value: 0.00,
      beizhu: ' ',
      startDate: '2018-05-9',
      endDate: '2018-02-21',
      pickerStart: '2018-05-6'
    }
  },

  components: {

  },

  computed: {
    newMultiArray: () => {
      let array = []
      const date = new Date()
      const years = []
      const months = []
      const days = []
      for (let i = 2018; i <= date.getFullYear() + 10; i++) {
        years.push('' + i)
      }
      array.push(years)
      for (let i = 1; i <= 12; i++) {
        if (i < 10) {
          i = '0' + i
        }
        months.push('' + i)
      }
      array.push(months)
      for (let i = 1; i <= 31; i++) {
        if (i < 10) {
          i = '0' + i
        }
        days.push('' + i)
      }
      array.push(days)
      return array
    }
  },
  mounted () {
    let today = this.getToday()
    this.startDate = today
    this.endDate = today
    this.pickerStart = today
  },

  methods: {
    handleChangeScroll (detail) {
      console.log(detail.mp.detail.key)
      switch (detail.mp.detail.key) {
        case 'tab1':
          this.tab1 = true
          this.tab3 = false
          this.tab2 = false
          break
        case 'tab2':
          this.tab2 = true
          this.tab1 = false
          this.tab3 = false
          break
        case 'tab3':
          this.tab3 = true
          this.tab1 = false
          this.tab2 = false
          break
        default:
          break
      }
    },
    // 获取时间日期
    getToday () {
      let myDate = new Date()
      let myMonth = myDate.getMonth() + 1
      if (myMonth < 10) {
        myMonth = '0' + myMonth // 补齐
      }
      let mydate = myDate.getDate()
      if (myDate.getDate() < 10) {
        mydate = '0' + myDate.getDate() // 补齐
      }
      let today = myDate.getFullYear() + '-' + myMonth + '-' + mydate
      return today
    },
    bindDateChangeStart (e) {
      var this_ = this
      this_.startDate = e.mp.detail.value
      console.log(e)
    }
  }
}
</script>
<style>
#home {
  width: 100%;
  text-align: center;
  color: black;
}
.tab {
  text-align: center;
}
.input {
  border-bottom: 0.05rem black solid;
  margin-bottom: 0.1rem;
}
.center {
  margin-top: 0.2rem;
}
.tab1{
  font-size:0.3rem;
}

</style>
