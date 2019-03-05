<template>
  <div>
    <scroll-view :style="{'height': '380px'}" :scroll-y="true" @scrolltolower="scrolltolower" @scroll="scroll">
    <i-cell-group>
      <i-cell v-for="t in list" :key="index"  :title="t.category" :label="t.date" :value="t.amount"  is-link url="/pages/detail/main">
        <text>{{t.remarks}}</text>
      </i-cell>
    </i-cell-group>
    </scroll-view>
  </div>
</template>

<script>
export default {
  props: ['list'],
  methods: {
    scrolltolower () {
      console.log(7)
    },
    scroll (e) {
      console.log(6)
      console.log(e)
    }

  }
}
</script>

<style>
  .card {
    padding: 10px;
  }
</style>
