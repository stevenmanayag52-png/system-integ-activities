<template>
  <div ref="mapContainer" class="map-container"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import L from 'leaflet'
import 'leaflet/dist/leaflet.css'


import icon from 'leaflet/dist/images/marker-icon.png'
import iconShadow from 'leaflet/dist/images/marker-shadow.png'

const mapContainer = ref<HTMLElement | null>(null)
let map: L.Map | null = null

onMounted(() => {
  if (!mapContainer.value) return

  // Apply icon fix
  const DefaultIcon = L.icon({
    iconUrl: icon,
    shadowUrl: iconShadow,
    iconSize: [25, 41],
    iconAnchor: [12, 41],
  })
  L.Marker.prototype.options.icon = DefaultIcon

  // Initialize Map
  map = L.map(mapContainer.value).setView([15.1833, 120.5333], 10)

  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap'
  }).addTo(map)
})

onUnmounted(() => {
  if (map) {
    map.remove()
  }
})
</script>


<style scoped>
.map-container {
  height: 400px;
  width: 100%;
}
</style>