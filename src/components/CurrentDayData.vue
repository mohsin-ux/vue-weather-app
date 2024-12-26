
<script setup lang="ts">
 const {singleDay} = defineProps<
 {
   singleDay: any
 }
 >()
</script>
<template>
    <div>
        <p class="font-bold">
          Temperature: <span class="font-normal">{{ singleDay.temp }} &deg;C</span>
        </p>
        <p class="font-bold">
          Date: <span class="font-normal">{{ singleDay.datetime }}</span>
        </p>
        <p class="font-bold">
          Condition: <span class="font-normal">{{ singleDay.conditions }}</span>
        </p>
        <p class="font-bold">
          Humidity:
          <span class="font-normal">{{ singleDay.humidity }} g/m&sup3</span>
        </p>
        <p class="font-bold">
          Wind: <span class="font-normal">{{ singleDay.windspeed }} mph</span>
        </p>
        <p class="font-bold">
          Min temperature:
          <span class="font-normal">{{ singleDay.tempmin }} &deg;C</span>
        </p>
        <p class="font-bold">
          Max temperature:
          <span class="font-normal">{{ singleDay.tempmax }} &deg;C</span>
        </p>
        <p class="font-bold">
          Description:
          <span class="font-normal">{{ singleDay.description }}</span>
        </p>
    </div>

</template>
