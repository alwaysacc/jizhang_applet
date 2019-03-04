<template>
  <div class="top">
    <a>本{{msg}}支出</a>
    <a style="font-size:2rem">0.00</a>
    <div class="top2">
        <span>
          <text>本{{msg}}收入:</text>
          <text>0</text>
        </span>
      <span style="padding-left: 5rem;">
          <text>本{{msg}}盈余:</text>
          <text>0</text>
        </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'top',
  props: ['msg']
}
</script>

<style scoped>

  a {
    font-size: 0.3rem;
  }
  .top {
    padding-top: 1rem;
    height: 2.3rem;
    background-color: #fa7a1f;
    padding-left: 0.2rem;
  }
  .top2 {
    padding-top: 0.2rem;
    font-size: 0.3rem;
  }
</style>
