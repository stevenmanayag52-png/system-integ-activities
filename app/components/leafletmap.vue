<template>
  <div ref="mapContainer" class="map-container"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

import 'leaflet/dist/leaflet.css'
import L from 'leaflet'


const mapContainer = ref<HTMLElement | null>(null)


let map: L.Map | null = null

onMounted(() => {
  if (!mapContainer.value) return

  
  map = L.map(mapContainer.value).setView([15.223, 120.590], 12)

  
  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
  }).addTo(map)

  // 3. Optional: Add a custom marker
  L.marker([15.223, 120.590])
    .addTo(map)
    .bindPopup('<b>St.nicolas college   </b><br>Rendered via Vue Component.')
    .openPopup()
})

onUnmounted(() => {
 
  if (map) {
    map.remove()
    map = null
  }
})
</script>

<style scoped>
.map-container {
  height: 500px;
  width: 100%;
  border-radius: 8px; 
  z-index: 1; 
}
</style>
