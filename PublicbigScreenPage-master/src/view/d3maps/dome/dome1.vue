 
<template>
  <div class="doms">
    <div id="three-frame"></div>
    <div class="echartbox">
      <Comps></Comps>
    </div>
  </div>
</template>

<script lang="ts" setup>
import Comps from './comps.vue';
// 圆盘地盘 地盘动画
import Render3DMode from './uselib/useThree1';
import { onMounted } from 'vue';
import { getGeoJsonall } from '@/lib/getGeoJson';
let { initMaps, setMapDom, setmapborder } = Render3DMode('three-frame');
let AreaCode = '100000'
onMounted(() => {
  initMaps();
  getGeoJsonall(`${AreaCode}_full`).then((e) => {
    setMapDom(e.data.features);
  });
  getGeoJsonall(AreaCode).then((e) => {
    // console.log()
    setmapborder(e.data.features);
  });
});
</script>

<style>
#three-frame {
  width: 100vw;
  height: 100vh;
}
.doms {
  width: 100vw;
  height: 100vh;
  background: #4d5353;
}
.echartbox {
  width: 100vw;
  height: 100vh;
  position: fixed;
  /* background: rgba(153, 150, 150, 0.738); */
  top: 0;
  left: 0;
  pointer-events: none;
}
</style>
