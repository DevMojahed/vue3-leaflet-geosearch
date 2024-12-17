<template>
  <div id="map" style="height:400px; width:500px">
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue"
// leaflet
import * as L from "leaflet"
import * as GeoSearch from 'leaflet-geosearch'
// styles
import "leaflet/dist/leaflet.css"
import 'leaflet-geosearch/dist/geosearch.css'

const zoom = ref(5)
const location = ref([33, 53])

onMounted(() => {
  const map = L.map('map').setView(location.value, zoom.value)

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map)

  const search = new GeoSearch.GeoSearchControl({
    style: 'bar',
    notFoundMessage: 'متاسفانه آدرسی پیدا نشد!',
    provider: new GeoSearch.OpenStreetMapProvider(),
  })

  map.addControl(search)
})
</script>