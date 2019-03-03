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
      <div v-if="tab1" class="input">
        <i-input v-model="value" type="number" />
      </div>
      <div v-if="tab2">2</div>
      <div v-if="tab3">3</div>
    </div>
    <i-row class="tab">
      <i-col span="4" i-class="col-class" v-for="t in tab" :key="t.id">{{t.name}}</i-col>
    </i-row>

  </div>
</template>

<script>
export default {
  data () {
    return {
      current: 'tab1',
      tab1: '',
      tab2: '',
      tab3: '',
      value: 0.001
    }
  },

  components: {

  },

  computed: {},

  mounted: {},

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
    }
  }
}
</script>
<style>
#home {
  width: 100%;
  text-align: center;
}
.tab {
  text-align: center;
}
.tab .input {
  border-bottom: 1rem black solid;
}
.center {
  margin-top: 0.2rem;
}
</style>