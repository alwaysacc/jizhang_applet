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
        <li ><img src="../../assets/money.png">现金<span>0</span></li>
        <li><img src="../../assets/bank.png">银行卡<span>0</span></li>
        <li><img src="../../assets/card.png">信用卡<span>0</span></li>
        <li><img src="../../assets/ali.png">支付宝<span>0</span></li>
        <li><img src="../../assets/weixin.png">微信钱包<span>0</span></li>
        <li><img src="../../assets/huabei.png">花呗<span>0</span></li>
        <li><img src="../../assets/baitiao.png">京东白条<span>0</span></li>
        <li><img src="../../assets/qita.png">其它<span>0</span></li>
      </ul>

    </div>
  </div>
</template>

<script>
export default {
  name: 'assets'
}
</script>

<style scoped>
  .header{
    text-align: center;
    height: 3rem;
    background-color: white;
  }
.top{
  padding-top: 0.4rem;
  font-size: 0.4rem;
  text-align: center;
  padding-bottom: 0.6rem;
}
  .header .bot span{
    display: block;
    font-size: 0.3rem;
  }
 img{
    width: 2rem;
    height: 2rem;
  }
  .bottom ul li{
    height: 1.2rem;
    line-height: 1rem;
    padding-left: 0.3rem;
    margin-top: 0.1rem;
    background-color: white;
  }
  .bottom ul li img{
    vertical-align: middle;
    height:1rem;
    width: 1rem;
    padding-right: 0.2rem;
  }
  .bottom ul li span{
    float: right;
    padding-right: 0.5rem;
  }
</style>
