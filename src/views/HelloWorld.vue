<script setup lang="ts">
import { ref, onMounted } from "vue";
import Cards from "../components/Cards.vue";
import Input from "../components/Input.vue";
const forecast = ref<any>();
const currentDay = ref<any>();

async function getWeather(latitude: string, longitude: string) {
  await fetch(
    `https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${latitude},${longitude}?key=DKALY8YWYJLB56BSTLZHTNV8P`
  )
    .then((response) => response.json())
    .then((data) => {
      console.log(data);
      forecast.value = data.days.filter((day: any, index: number) => index < 5);
      currentDay.value = forecast.value[0];
    })
    .catch((error) => console.error(error.message));
}
</script>

<template>
  <main class="bg-gradient-to-r from-cyan-500 to-blue-500 px-28 w-sreen h-screen">
    <Input @getWeather="getWeather" />
    <div class="border">
      <p class="font-bold">Current Day</p>
      <Cards :single-day="currentDay" />
    </div>

    <div class="flex flex-wrap">
      <div
        v-for="(singleDay, index) in forecast"
        class="w-[300px] border p-3 rounded-2xl"
      >
        <Cards v-if="index < 5" :single-day="singleDay" />
      </div>
    </div> 
  </main>
</template>

<style scoped></style>
