<script setup lang="ts">
import { useRoute } from "vue-router";

const route = useRoute();
</script>

<template>
  <div>
    <h1 class="text-blue-600">Task Id : {{ route.params?.id }}</h1>
    <RouterLink to="/tasks">Go To Tasks</RouterLink>
  </div>
</template>
