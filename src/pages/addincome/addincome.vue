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
        <input type="number" v-model="income.amount"  class="input"/>
        <i-grid @click="setCategory">
          <i-grid-item @click="a">一日三餐</i-grid-item>
          <i-grid-item>交通出行</i-grid-item>
          <i-grid-item>其他</i-grid-item>
        </i-grid>
        <i-input v-model="income.remarks" type="text" @change="setRemarks" title="备注：" maxlength="20" placeholder="请输入备注"/>
        <i-input v-model="income.address" title="地址：" type="text" @change="setAddress" maxlength="20"  placeholder="请输入地址"/>
        <i-input v-model="account" title="账户：" type="text"  @click="zhanghu"/>
        <i-modal :visible="visible4" :actions="actions4" action-mode="vertical" @click="setAccount">
        </i-modal>
        <picker mode="date"
                :value="income.dates"
                :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="income.dates" title="时间："></i-input>
          </div>
        </picker>
        <i-button @click="addOutlay" type="primary" size="large">保存</i-button>
        <i-toast id="toast" />
      </div>
      <div v-if="tab2">
        <input type="number" v-model="income.amount"  class="input"/>
        <i-grid @click="setCategory">
          <i-grid-item>工资</i-grid-item>
          <i-grid-item>理财</i-grid-item>
          <i-grid-item>其他</i-grid-item>
        </i-grid>
        <i-input v-model="income.remarks" type="textarea" @change="setRemarks" title="备注：" placeholder="请输入备注"/>
        <i-input v-model="income.address" title="地址：" type="textarea" @change="setAddress"  placeholder="请输入地址"/>
        <i-input v-model="account" title="账户：" type="text"  @click="zhanghu"/>
        <i-modal :visible="visible4" :actions="actions4" action-mode="vertical" @click="setAccount">
        </i-modal>
        <picker mode="date"
                :value="income.dates"
                :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="income.dates" title="时间："></i-input>
          </div>
        </picker>
        <i-button @click="addOutlay" type="primary" size="large">保存</i-button>
        <i-toast id="toast" />
      </div>
      <div v-if="tab3">
        <input type="number" v-model="income.amount"  class="input"/>
        <i-input :value="income.category" title="收款人" type="text"  />
        <i-input :bindtap="income.remarks" type="textarea" @change="setRemarks" title="备注：" placeholder="请输入备注"/>
        <i-input v-model="income.address" title="地址：" type="textarea" @change="setAddress"  placeholder="请输入地址"/>
        <i-input v-model="account" title="账户：" type="text"  @click="zhanghu"/>
        <i-modal :visible="visible4" :actions="actions4" action-mode="vertical" @click="setAccount">
        </i-modal>
        <picker mode="date"
                :value="income.dates"
                :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
          <div class="index_picker">
            <i-input :value="income.dates" title="时间："></i-input>
          </div>
        </picker>
        <i-button @click="addOutlay" type="primary" size="large">保存</i-button>
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
      visible4: false,
      income: {
        amount: '',
        category: '',
        address: '',
        dates: '',
        remarks: '',
        type: 1,
        account: '花呗',
        userid: ''
      },
      account: '花呗',
      actions4: [
        {
          name: '现金'
        },
        {
          name: '支付宝'
        },
        {
          name: '微信钱包'
        },
        {
          name: '银行卡'
        },
        {
          name: '信用卡'
        },
        {
          name: '花呗'
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
    this.income.dates = today
  },

  methods: {
    handleChangeScroll (detail) {
      console.log(detail.mp.detail.key)
      switch (detail.mp.detail.key) {
        case 'tab1':
          this.current = 'tab1'
          this.income.type = 1
          this.tab1 = true
          this.tab3 = false
          this.tab2 = false
          break
        case 'tab2':
          this.current = 'tab2'
          this.income.type = 2
          this.tab2 = true
          this.tab1 = false
          this.tab3 = false
          break
        case 'tab3':
          this.current = 'tab3'
          this.income.type = 3
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
      this_.income.dates = e.mp.detail.value
      console.log(e)
    },
    zhanghu () {
      this.visible4 = true
    },
    setAccount (e) {
      this.visible4 = false
      this.account = e.mp._relatedInfo.anchorRelatedText
      this.income.account = e.mp._relatedInfo.anchorRelatedText
      console.log(e)
    },
    // 添加支出
    addOutlay () {
      let t = this
      const user = wx.getStorageSync('user')
      t.income.userid = user.id
      console.log(t.income)
      t.$http.post({
        url: 'income/add',
        data: {
          incomeOutlay: JSON.stringify(t.income)
        }
      }).then(res => {
        console.log(res)
        if (res.data.code === 200) {
          $Toast({
            content: '成功',
            type: 'success'
          })
          t.income.remarks = ''
          t.income.category = ''
          t.income.address = ''
          t.income.amount = ''
        } else {
          $Toast({
            content: '请重试',
            type: 'info'
          })
        }
      })
    },
    setCategory (e) {
      console.log(e)
      this.income.category = e.mp._relatedInfo.anchorTargetText
    },
    setRemarks (e) {
      console.log(e.mp.detail.detail.value)
      this.income.remarks = e.mp.detail.detail.value
    },
    setAddress (e) {
      console.log(e.mp.detail.detail.value)
      this.income.address = e.mp.detail.detail.value
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
.ul li{
  float: left;
  width: 30%;
  margin-left: 3%;
}
</style>
