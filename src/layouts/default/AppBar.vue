<template>
  <v-app-bar flat class="bg-red">
    <v-app-bar-title>
      <!-- <v-icon icon="mdi-circle-slice-6" /> -->
      <div class="d-flex justify-center">
        <div
          style="cursor: pointer"
          class="px-4"
          @click="$router.push({ name: 'home' })"
        >
          Dashboard
        </div>
        <div
          style="cursor: pointer"
          @click="$router.push({ name: 'my-chart' })"
          class="px-4"
        >
          Chart
        </div>
      </div>
    </v-app-bar-title>
  </v-app-bar>
</template>

<script setup>
//
</script>
