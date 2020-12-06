<template>
  <div class="grid m-2 gap-2 fixed grid-rows--5 "
    :style=styles
  >
    <div class="box-fill w-full h-full bg-gray-100 row-start-1 row-end-2"></div>
    <div class="box-logo w-full h-full bg-green-300 col-start-1 "></div>
    <!-- condidion boxes -->
    <div class="box-navi-1 w-full h-full bg-gray-600 "></div>
    <div class="box-navi-2 w-full h-full bg-gray-500 "></div>
    <div class="box-navi-3 w-full h-full bg-gray-400 "></div>
    <div class="box-navi-4 w-full h-full bg-gray-300 "></div>
    <div class="box-navi-5 w-full h-full bg-gray-200 "></div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

// import HelloWorld from './components/HelloWorld.vue'

export default defineComponent({
  components: {},
  data(){
    return {
      boxNumber: 2,
      boxWidths: [3,4,5],
      pxSizes: {
        firstCol: 160,
        colMax: 3,
        rowMax: 5,
        lastRow: 100,
      }
    }
  },
  computed: {
    naviWidth(data) {
      if ( data.boxNumber >= 5 )
        return `width: calc(${data.pxSizes.firstCol/16}rem +  ${100/16 * data.boxNumber}rem + ${8 / 16 * (data.boxNumber)}rem)`;
      return `width: calc(${data.pxSizes.firstCol/16}rem +  ${100/16 * data.boxNumber}rem + ${8 / 16 * (data.boxNumber+1)}rem)`;
    },
    // maxColumn(data){
    //   return `col-start-1 col-end-${data.boxNumber+1}`;
    // },
    columnsTemp(data) {
      if ( data.boxNumber >= 5 )
        return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr 1fr 1fr 1fr`;
      if ( data.boxNumber == 4 )
        return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr 1fr 1fr`;
      else if ( data.boxNumber == 3 )
        return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr 1fr`;

      return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr`;
    },
    styles(data){
      return `${data.naviWidth}; ${data.columnsTemp}`
    }
  },
  methods: {
    detectBoxNumber(){
      const _arrWidths = this.boxWidths.filter((elem)=>{ return elem < window.innerWidth});
      this.boxNumber = _arrWidths.length + 2;
      return this.boxNumber;
    }
  },
  mounted() {
    this.boxWidths = this.boxWidths.map((num)=>{ return this.pxSizes.firstCol + 100 * num + 8 * (num + 1) });
    this.detectBoxNumber();
    //
    window.addEventListener('resize',this.detectBoxNumber);
  }, 
  unmounted(){
    window.removeEventListener('resize', this.detectBoxNumber);
  }
})
</script>
<style>
.grid {
  grid-template-columns: 160px 1fr 1fr;
  grid-template-rows: 1fr 100px;
  width: calc(160px + 100px * 2 + 8px * 2);
}
.h-full.box-fill {
  grid-column: 1/-1;
  height: calc(100vh - ( 100px + 3*8px));
}
</style>
