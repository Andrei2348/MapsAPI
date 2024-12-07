<template>
  <div>
    <button @click="getLocation" class="button">Получить вашу локацию и добавить маркер</button>
    <p>
      Ваши координаты: {{ lat }} and {{ lng }}
    </p>
    <div ref="mapContainer" class="map"></div>
  </div>
</template>

<script lang="ts" setup>
import { onBeforeMount, onMounted, ref } from 'vue'
import L from 'leaflet'

const lat = ref<number>( 55.7558)
const lng = ref<number>(37.6173)
const map = ref()
const mapContainer = ref()

function getLocation() {  
  if (navigator.geolocation) {  
    navigator.geolocation.getCurrentPosition((position) => {  
      lat.value = position.coords.latitude;  
      lng.value = position.coords.longitude;   
      map.value.setView([lat.value, lng.value], 13);  
      L.marker([lat.value, lng.value], { draggable: true })  
        .addTo(map.value) 
    });  
  }  
}

onBeforeMount(() => {  
  if (navigator.geolocation) {  
    navigator.geolocation.getCurrentPosition((position) => {  
      lat.value = position.coords.latitude;  
      lng.value = position.coords.longitude;  
      console.log(lat.value, lng.value)
    }) 
  }  
})

onMounted(() => {
  map.value = L.map(mapContainer.value).setView([lat.value, lng.value], 13);

  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
}).addTo(map.value);
})
</script>
<style lang="scss" scoped>
.map{
  height: 800px;
  width: 800px;
}
.button{
  @include primaryButton;
}
</style>
