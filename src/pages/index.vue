<script setup lang="ts">
import { RouterLink } from "vue-router";
</script>

<template>
  <div>
    <h1 class="text-red-600">Home Page</h1>
    <RouterLink :to="{ name: '/projects/[id]', params: { 'id': 1 } }">Go To Projects</RouterLink>
  </div>
</template>
