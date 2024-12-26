<script setup lang="ts">
const { singleDay } = defineProps<{
  singleDay: any;
}>();

</script>
<template>
  <main>
    <div>
      <i class="fa fa-sun-o"></i>
      <p>{{ singleDay.icon }}</p>
      <p>Date: {{ singleDay.datetime.slice(8, 10) }}</p>
      <p>Max temperature: {{ singleDay.tempmax }}</p>
      <p>Min temperature: {{ singleDay.tempmin }}</p>
    </div>
  </main>
</template>
