<template>
  <div>
    <scroll-view :style="{'height': '15rem'}" :scroll-y="true" @scrolltolower="scrolltolower" @scroll="scroll">
    <i-cell-group>
      <i-cell v-for="t in list" :key="index"  :title="t.category" :label="t.dates" :value="t.amount" @click="toDetail(t.id,t.type)"  is-link>
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
    },
    toDetail (e1, e2) {
      const url = '../detail/main?id=' + e1 + '&&type=' + e2
      mpvue.navigateTo({ url })
      console.log(e1)
      console.log(e2)
    }

  }
}
</script>

<style>
</style>
