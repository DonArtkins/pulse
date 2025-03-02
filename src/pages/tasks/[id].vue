<script setup lang="ts">
import { usePageStore } from "@/stores/page";
import { useRoute } from "vue-router";

usePageStore().pageData.title = 'Tasks Details'

const route = useRoute();
</script>

<template>
  <div>
    <h1>Task {{ route.params?.id }}</h1>
  </div>
</template>
