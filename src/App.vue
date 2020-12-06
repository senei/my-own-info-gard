<template>
  <BoxNavi :maxNum="boxNumber" :widths="boxWidths"></BoxNavi>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BoxNavi from './components/BoxNavi.vue'
// import HelloWorld from './components/HelloWorld.vue'

export default defineComponent({
  components: { BoxNavi },
  data() {
    return {
      boxNumber: 2,
      boxWidths: [3, 4, 5],
      pxSizes: {
        firstCol: 160,
        colMax: 3,
        rowMax: 5,
        lastRow: 100,
      },
    }
  },
  methods: {
    detectBoxNumber() {
      const _arrWidths = this.boxWidths.filter((elem) => {
        return elem < window.innerWidth
      })
      this.boxNumber = _arrWidths.length + 2;
      return this.boxNumber
    },
  },
  beforeMount() {
    this.boxWidths = this.boxWidths.map((num) => {
      return this.pxSizes.firstCol + 100 * num + 8 * (num + 1)
    })
    this.detectBoxNumber()
  },
  mounted() {
    window.addEventListener('resize', this.detectBoxNumber)
  },
  unmounted() {
    window.removeEventListener('resize', this.detectBoxNumber)
  },
})
</script>
<style>
</style>
