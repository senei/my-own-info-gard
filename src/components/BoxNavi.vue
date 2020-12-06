<template>
<div class="grid m-2 gap-2  grid-rows--5 "
    :style=styles
  >
    <div class="box-fill w-full h-full bg-gray-100 row-start-1 row-end-2">
      {{widths?widths:'this.widths'}}{{maxNum?maxNum:'this.maxNum'}}
    </div>
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
import {
  defineComponent
} from 'vue'

export default defineComponent({
  components: {},
  props:{
    widths: Array, 
    maxNum: Number
  },
  data(){
    return {
      pxSizes: {
        firstCol: 160,
        colMax: 3,
        rowMax: 5,
        lastRow: 100,
      }
    }
  },
  computed: {
    naviWidth(data: { maxNum: number; pxSizes: { firstCol: number; }; }) {
      if ( data.maxNum >= 5 )
        return `width: calc(${data.pxSizes.firstCol/16}rem +  ${100/16 * data.maxNum}rem + ${8 / 16 * (data.maxNum)}rem)`;
      return `width: calc(${data.pxSizes.firstCol/16}rem +  ${100/16 * data.maxNum}rem + ${8 / 16 * (data.maxNum+1)}rem)`;
    },
    columnsTemp(data: { maxNum: number; pxSizes: { firstCol: number; }; }) {
      if ( data.maxNum >= 5 )
        return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr 1fr 1fr 1fr`;
      if ( data.maxNum == 4 )
        return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr 1fr 1fr`;
      else if ( data.maxNum == 3 )
        return `grid-template-columns: ${data.pxSizes.firstCol/16}rem 1fr 1fr 1fr`;
      //
      return `grid-template-columns: 1.2fr 1fr 1fr; grid-template-rows: 1fr 90px;`;
    },
    styles(){
      return `${this.naviWidth}; ${this.columnsTemp}`
    }
  }
})
</script>
<style>
.grid {
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr 100px;
  width: calc(160px + 100px * 2 + 8px * 2);
}
.h-full.box-fill {
  grid-column: 1/-1;
}
</style>
