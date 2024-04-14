<template>
  <div id="map-container">
    <div id="map" ref="mapRef" />
  </div>
</template>

<script>
import Radar from 'radar-sdk-js'
import { shallowRef, onMounted, onUnmounted, markRaw } from 'vue'

export default {
  name: 'RadarMap',
  setup() {
    const mapRef = shallowRef(null)
    const map = shallowRef(null)

    onMounted(() => {
      Radar.initialize('prj_live_pk_4fa29c7ab8d33d669b2ccd9b034f51addc537621')

      // create a map
      map.value = markRaw(
        Radar.ui.map({
          container: mapRef.value,
          style: 'radar-dark-v1',
          center: [25.02791, 58.80824],
          zoom: 6.39412
        })
      )

      // add a marker to the map
      Radar.ui.marker({ color: '#007aff' })
      .setLngLat([-73.9911, 40.7342])
      .addTo(map.value);
    }),
      onUnmounted(() => {
        map.value?.remove()
      })

    return {
      map,
      mapRef
    }
  }
}
</script>

<style>
@import 'radar-sdk-js/dist/radar.css';

body {
  margin: 0;
  padding: 0;
}

#map-container {
  height: 100%;
  position: absolute;
  width: 100%;
}

#map {
  height: 100%;
  position: absolute;
  width: 100%;
}
</style>
