<template>
  <div id="home">
    <div class="bot">
      <i-input v-model="income.amount" title="金额：" type="textarea" @change="setAmount" />
      <i-input v-model="income.category" :title="name" type="textarea" @change="setCategory" />
      <i-input v-model="income.remarks" title="备注：" type="textarea" @change="setRemarks"  />
      <i-input v-model="income.address" title="地址：" type="textarea" @change="setAddress"  />
      <i-input v-model="income.account" title="账户：" type="text"  @click="zhanghu" />
      <i-modal :visible="visible4" :actions="actions4" action-mode="vertical" @click="sAccount"></i-modal>
      <picker mode="date"
              :value="income.dates"
              :start="pickerStart" end="2217-09-01" @change="bindDateChangeStart($event)">
        <div class="index_picker">
          <i-input :value="income.dates" title="时间："></i-input>
        </div>
      </picker>
    </div>
    <div class="but">
      <button @click="deleteIncome" class="btn">删除</button>
      <button @click="updateIncome" class="btn">修改</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'detial',
  data () {
    return {
      title: '',
      name: '',
      income: {
      },
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
      ],
      visible4: false
    }
  },
  components: {
  },
  methods: {
    deleteIncome () {
      let t = this
      t.$http.post({
        url: 'income/delete',
        data: {
          id: t.income.id
        }
      }).then(res => {
        console.log(res)
      })
    },
    updateIncome () {
      let t = this
      console.log(t.income)
      t.$http.post({
        url: 'income/update',
        data: {
          incomeOutlay: JSON.stringify(t.income)
        }
      }).then(res => {
        console.log(res)
      })
    },
    bindDateChangeStart (e) {
      var this_ = this
      this_.income.dates = e.mp.detail.value
      console.log(e)
    },
    getDetail (e) {
      let t = this
      t.$http.post({
        url: 'income/detail',
        data: {
          id: e
        }
      }).then(res => {
        console.log(res)
        t.income = res.data.data
      })
    },
    setAmount (e) {
      console.log(e)
      this.income.amount = e.mp.detail.detail.value
    },
    setCategory (e) {
      this.income.category = e.mp.detail.detail.value
    },
    setRemarks (e) {
      console.log(e.mp.detail.detail.value)
      this.income.remarks = e.mp.detail.detail.value
    },
    setAddress (e) {
      console.log(e.mp.detail.detail.value)
      this.income.address = e.mp.detail.detail.value
    },
    zhanghu () {
      this.visible4 = true
    },
    sAccount (e) {
      this.visible4 = false
      this.income.account = e.mp._relatedInfo.anchorRelatedText
      console.log(e)
    }
  },
  onLoad: function (e) {
    let t = this
    t.getDetail(e.id)
    switch (e.type) {
      case '1':
        t.title = '支出详情'
        t.name = '类型：'
        break
      case '2':
        t.title = '收入详情'
        t.name = '类型：'
        break
      case '3':
        t.title = '转账详情'
        t.name = '收款人：'
        break
    }
    wx.setNavigationBarTitle({
      title: t.title,
      success: function (res) {
        // success
      }
    })
  },
  onShow: function (e) {
    // console.log(e)
  }
}
</script>

<style scoped>
#home{
  margin: 0rem;
  padding: 0rem;
  text-align: center;
  width: 100%;
}
  .top{
    height: 2rem;
    width: 100%;
    line-height: 2rem;
    background-color: white;
  }
  .bot{
    padding-top: 0.2rem;
    text-align: center;
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
