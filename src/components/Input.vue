<script setup lang="ts">
import { ref, onMounted } from "vue";
const latitude = ref<string>("");
const longitude = ref<string>("");
const city = ref<string>("Washington");

const emits = defineEmits<{
  (e: 'getWeather', latitude: string, longitude: string): void,
}>();

async function getLocation() {
  await fetch(
    `https://nominatim.openstreetmap.org/search?q=${city.value}&format=json&limit=1`
  )
    .then((response) => response.json())
    .then((data) => {
      if (data.length > 0) {
        const { lat, lon } = data[0];
        latitude.value = lat;
        longitude.value = lon;
        console.log(`Latitude: ${lat}, Longitude: ${lon}`);
      } else {
        console.error("Location not found!");
      }
    })
    .catch((error) => console.error("Error:", error));
  emits('getWeather', latitude.value, longitude.value);
}
onMounted(() => {
  getLocation();
});
</script>

<template>
  <form
    @submit.prevent="getLocation"
    class="border flex flex-col items-start"
  >
    <label for="temp">Enter location</label>
    <input class="border" type="text" v-model="city" id="temp" />
    <button class="border rounded">submit</button>
  </form>


</template>
