<script setup>

import { ref, onMounted } from 'vue'

import XYZ from 'ol/source/XYZ';

import {Map, View} from 'ol';
import Tile from 'ol/layer/Tile';
import OSM from 'ol/source/OSM';
import {fromLonLat} from 'ol/proj.js';
import {ScaleLine} from 'ol/control.js';
import MousePosition from 'ol/control/MousePosition.js';
import {createStringXY} from 'ol/coordinate.js';
import {defaults as defaultControls} from 'ol/control.js';


const map = ref(null)
const initMap =() =>{
  // 地图实例
  map.value = new Map({
    
    target: 'map',                         // 对应页面里 id 为 map 的元素
    layers: [                              // 图层
      new Tile({                           // 使用瓦片渲染方法
        // source: new OSM()                  // 图层数据源
        source: new XYZ({
        url: 'http://mt0.google.com/vt/lyrs=m&hl=en&x={x}&y={y}&z={z}'
      })
      })
    ],
    view: new View({                       // 地图视图
      projection: "EPSG:4326",             // 坐标系，有EPSG:4326和EPSG:3857
      center: [120, 23.488793],     // 台灣坐标
                                           // 地图缩放最小级别
      zoom: 8                             // 地图缩放级别（打开页面时默认级别）
    }),
    controls: []
  }),
  map.addControl(
    new ScaleLine({
        // {'degrees'} {'imperial'} {'nautical'} {'metric'} {'us'}
        // 比例尺有提供幾種單位可以調整，範例如下
        // units: 'us'
        bar: true,
        steps: 4
    }))

}

onMounted(() => {
  initMap()
})

</script>

<template>
    <div id="map" class="map__x"></div>
</template>

<style scoped>
html, body {
  /* margin: 0;
  height: 100%; */
}
#map {
  /* position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  z-index: 0; */
  /* height: 600px; */
  width: 1000px;
  height: 600px;
}
.ol-zoom-in{
  width: 10px;
}
</style>