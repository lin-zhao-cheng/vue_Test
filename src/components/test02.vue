<script setup>
import {  onMounted } from 'vue'
import {Map, View} from 'ol';
import TileLayer from 'ol/layer/Tile';
import OSM from 'ol/source/OSM';
import {fromLonLat} from 'ol/proj.js';
import {ScaleLine} from 'ol/control.js';
import MousePosition from 'ol/control/MousePosition.js';
import {createStringXY} from 'ol/coordinate.js';
import {defaults as defaultControls} from 'ol/control.js';




const map = ref(null)
const initMap =() =>{
  const taiwan=[120.846642, 23.488793];
  const taiwanwebMercator=fromLonLat(taiwan);

  const mousePositionControl = new MousePosition({
  coordinateFormat: createStringXY(4),
  projection: 'EPSG:4326',
  className: 'custom-mouse-position',
  target: document.getElementById('mouse-position'),
  
});


const map = new Map({
  controls: defaultControls().extend([mousePositionControl]),
  target: 'map',
  layers: [
    new TileLayer({
       source: new OSM()
    }),

  ],
  view: new View({
    center: taiwanwebMercator,
    zoom: 7
  }),
  // controls: []
  
});
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
  width: 600px;
  height: 600px;
}
</style>