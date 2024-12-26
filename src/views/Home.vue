<script setup lang="ts">
import { ref, onMounted } from "vue";
import Input from "../components/Input.vue";
import CurrentDayData from "../components/CurrentDayData.vue";
import SingleCard from "../components/SingleCard.vue";
const forecast = ref<any>();
const currentDay = ref<any>();

async function getWeather(latitude: string, longitude: string) {
  await fetch(
    `https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/${latitude},${longitude}?key=DKALY8YWYJLB56BSTLZHTNV8P&unitGroup=metric`
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
  <main
    class="bg-gradient-to-r from-cyan-500 to-blue-500 px-28 py-10 w-sreen h-screen"
  >
  <div class="flex flex-col gap-3">
      <div>
        <h1 class="text-4xl font-bold text-white">Weather App</h1>
      </div>
      <Input @getWeather="getWeather" />
      <div class=" w-full h-screen flex justify-center items-center" v-if="!forecast">
        <div
          class="w-16 h-16 border-4 border-gray-300 border-t-blue-500 rounded-full animate-spin"
        ></div>
      </div>
      <div v-else class="flex flex-col gap-3">
        <div class="border bg-emerald-900 text-white p-3 rounded-lg">
          <CurrentDayData :single-day="currentDay" />
        </div>

        <div class="flex flex-wrap gap-2">
          <div
            v-for="(singleDay, index) in forecast"
            class="w-[200px] border p-3 rounded-2xl bg-blue-800 text-white"
          >
            <SingleCard :singleDay="singleDay" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
