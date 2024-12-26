<script setup lang="ts">
const { singleDay } = defineProps<{
  singleDay: any;
}>();

</script>
<template>
  <main>
    <div>
      <i class="fa fa-sun-o"></i>
      <p>Date: {{ singleDay.datetime.slice(8, 10) }}</p>
      <p>Max temp: {{ singleDay.tempmax }} &deg;C</p>
      <p>Min temp: {{ singleDay.tempmin }} &deg;C</p>
    </div>
  </main>
</template>
