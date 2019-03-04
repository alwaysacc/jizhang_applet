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
        <i-input value="alue4" title="地址：" type="text"  />
        <i-input value="alue4" title="账户：" type="text"  @click="zhanghu"/>
        <i-modal :visible="visible4" :actions="actions4" action-mode="vertical" @click="handleClick4">
        </i-modal>
        <picker mode="date"
                :value="startDate"
                :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="startDate" title="时间："  />
          </div>
        </picker>
        <i-button @click="addOutlay" type="primary" size="large">保存</i-button>
        <i-toast id="toast" />
      </div>
      <div v-if="tab2">
        <input type="number" v-model="value"  class="input"/>
        <i-grid>
          <i-grid-item>工资</i-grid-item>
          <i-grid-item>理财</i-grid-item>
          <i-grid-item>其他</i-grid-item>
        </i-grid>
        <i-input value="lue3" type="textarea" title="备注：" placeholder="请输入详细地址(最多50字)" maxlength="50" />
        <i-input value="alue4" title="地址：" type="text"  />
        <i-input value="alue4" title="账户：" type="text"  />
        <picker mode="date"
                :value="startDate"
                :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="startDate" title="时间："  />
          </div>
        </picker>
        <i-button @click="addIncome" type="primary" size="large">保存</i-button>
        <i-toast id="toast" />
      </div>
      <div v-if="tab3">
        <input type="number" v-model="value"  class="input"/>
        <i-input value="alue4" title="收款人" type="text"  />
        <i-input value="lue3" type="textarea" title="备注：" placeholder="请输入详细地址(最多50字)" maxlength="50" />
        <i-input value="alue4" title="地址：" type="text"  />
        <i-input value="alue4" title="账户：" type="text"  @click="zhanghu"/>
        <i-modal :visible="visible4" :actions="actions4" action-mode="vertical" @click="handleClick4">
        </i-modal>
        <picker mode="date"
                :value="startDate"
                :start="startDate" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="startDate" title="时间："  />
          </div>
        </picker>
        <i-button @click="addTransfer" type="primary" size="large">保存</i-button>
        <i-toast id="toast" />
      </div>
    </div>
  </div>
</template>

<script>
import {$Toast} from '../../../static/iView/base/index'
export default {
  data () {
    return {
      current: 'tab1',
      tab1: true,
      tab2: '',
      tab3: '',
      value: 0.00,
      beizhu: ' ',
      startDate: '',
      visible4: false,
      actions4: [
        {
          name: '按钮1'
        },
        {
          name: '按钮2',
          color: '#ff9900'
        },
        {
          name: '按钮3',
          icon: 'search'
        }
      ]

    }
  },

  components: {
    $Toast
  },

  computed: {
  },
  mounted () {
    let today = this.getToday()
    this.startDate = today
  },

  methods: {
    handleChangeScroll (detail) {
      console.log(detail.mp.detail.key)
      switch (detail.mp.detail.key) {
        case 'tab1':
          this.current = 'tab1'
          this.tab1 = true
          this.tab3 = false
          this.tab2 = false
          break
        case 'tab2':
          this.current = 'tab2'
          this.tab2 = true
          this.tab1 = false
          this.tab3 = false
          break
        case 'tab3':
          this.current = 'tab3'
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
    },
    zhanghu () {
      this.visible4 = true
    },
    handleClick4 (e) {
      this.visible4 = false
      console.log(e)
    },
    addOutlay () {
      console.log(1)
      $Toast({
        content: '成功的提示',
        type: 'success'
      })
    },
    addIncome () {
      console.log(1)
      $Toast({
        content: '成功的提示',
        type: 'success'
      })
    },
    addTransfer () {
      console.log(1)
      $Toast({
        content: '成功的提示',
        type: 'success'
      })
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
  border-bottom: 0.03rem black solid;
  margin-bottom: 0.1rem;
  font-size: 0.8rem;
  height: 1rem;
}
.center {
  margin-top: 0.2rem;
}
.tab1{
  font-size:0.3rem;
}

</style>
