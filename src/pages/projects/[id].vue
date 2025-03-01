<script setup lang="ts">
import { useRoute } from "vue-router";

const route = useRoute();
</script>

<template>
  <div>
    <h1 class="text-green-600">Project Id : {{ route.params?.id }}</h1>
  </div>
</template>
