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
        <span>总负债:</span>
        <span>近七日日均消费:</span>
        <span>近一月日均消费:</span>
      </div>
    </div>
    <div class="bottom">
      <i-cell-group>
        <i-cell title="显示箭头" value="555.0" is-link url="/pages/detail/main">
           <img src="https://i.loli.net/2017/08/21/599a521472424.jpg"/>
        </i-cell>
        <i-cell title="只显示箭头" label="2019年3月1日11:29:30" value="555.0">
          <text>666</text>
        </i-cell>
        <i-cell title="只显示箭头" label="2019年3月1日11:29:30" value="555.0">
          <text>666</text>
        </i-cell>
      </i-cell-group>
      <i-avatar size="large" shape="square">A</i-avatar>

      <i-avatar src="https://i.loli.net/2017/08/21/599a521472424.jpg" ></i-avatar>
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
  padding-top: 0.2rem;
  font-size: 0.5rem;
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
</style>
