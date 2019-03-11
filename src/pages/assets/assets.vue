<template>
  <div id="home">
    <div class="header">
      <div class="top">
         <span>
          <text>总资产:</text>
          <text>0</text>
        </span>
        <span style="padding-left: 5rem;">
          <text>净资产:</text>
          <text>0</text>
        </span>
      </div>
      <div class="bot">
        <span>近七日日均消费:</span>
        <span>近一月日均消费:</span>
      </div>
    </div>
    <div class="bottom">
      <ul>
        <li @click="goupdate"><img src="../../assets/money.png">现金<span>{{list.money}}</span></li>
        <li @click="goupdate"><img src="../../assets/bank.png">银行卡<span>{{list.bank}}</span></li>
        <li @click="goupdate"><img src="../../assets/card.png">信用卡<span>{{list.credit}}</span></li>
        <li @click="goupdate"><img src="../../assets/ali.png">支付宝<span>{{list.alipay}}</span></li>
        <li @click="goupdate"><img src="../../assets/weixin.png">微信钱包<span>{{list.wechat}}</span></li>
        <li @click="goupdate"><img src="../../assets/huabei.png">花呗<span>{{list.huabei}}</span></li>
        <li @click="goupdate"><img src="../../assets/baitiao.png">京东白条<span>{{list.jingdong}}</span></li>
        <li @click="goupdate"><img src="../../assets/qita.png">其它<span>{{list.other}}</span></li>
      </ul>
      <i-modal title="修改账户金额" :visible="visible1" @ok="update" @cancel="handleClose">
        <div style="text-align: center">
          <input type="number" v-model="num"  class="input" @click="clearInput"/>
        </div>
        <i-toast id="toast" />
      </i-modal>

    </div>
  </div>
</template>

<script>
import {$Toast} from '../../../static/iView/base/index'
export default {
  name: 'assets',
  data () {
    return {
      visible1: false,
      a: 123,
      list: '',
      num: '',
      column: '好好'
    }
  },
  components: {
    $Toast
  },
  methods: {
    clearInput () {
      console.log(11111)
      this.num = ''
    },
    setNum (e) {
      console.log(e)
    },
    goupdate (e) {
      this.visible1 = true
      this.num = e.mp._relatedInfo.anchorTargetText.replace(/[^0-9..]/ig, '')
      this.column = e.mp._relatedInfo.anchorTargetText.replace(/\d+/g, '')
      console.log(e.mp._relatedInfo.anchorTargetText.replace(/[^0-9]/ig, ''))
      console.log(e.mp._relatedInfo.anchorTargetText.replace())
      console.log(e)
    },
    update () {
      var t = this
      t.$http.post({
        url: 'account/update',
        data: {
          userid: wx.getStorageSync('user').id,
          num: t.num,
          column: t.column
        }
      }).then(res => {
        console.log(res.data)
        if (res.data.code === 200) {
          t.getList()
          $Toast({
            content: '成功',
            type: 'success'
          })
        } else {
          $Toast({
            content: '失败',
            type: 'info'
          })
        }
      })
      this.visible1 = false
    },
    handleClose () {
      this.visible1 = false
    },
    getList () {
      var t = this
      t.$http.post({
        url: 'account/detail',
        data: {
          userid: wx.getStorageSync('user').id
        }
      }).then(res => {
        if (res.data.code === 200) {
          t.list = res.data.data
        }
        console.log(res)
        console.log(t.list)
      })
    }
  },
  onReady () {
    this.getList()
  }
}
</script>

<style scoped>
  .header {
    text-align: center;
    height: 3rem;
    background-color: white;
  }

  .top {
    padding-top: 0.4rem;
    font-size: 0.4rem;
    text-align: center;
    padding-bottom: 0.6rem;
  }

  .header .bot span {
    display: block;
    font-size: 0.3rem;
  }

  img {
    width: 2rem;
    height: 2rem;
  }

  .bottom ul li {
    height: 1.2rem;
    line-height: 1rem;
    padding-left: 0.3rem;
    margin-top: 0.1rem;
    background-color: white;
    font-size: 0.3rem;
  }

  .bottom ul li img {
    vertical-align: middle;
    height: 1rem;
    width: 1rem;
    padding-right: 0.2rem;
  }

  .bottom ul li span {
    float: right;
    padding-right: 0.5rem;
  }
  .input{
    border-bottom: darkgrey 0.01rem solid;
  }
</style>
