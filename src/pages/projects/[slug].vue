<script setup lang="ts">
import { usePageStore } from '@/stores/page';
import { useRoute } from 'vue-router';

usePageStore().pageData.title = 'Projects Details'

const route = useRoute();
</script>

<template>
  <div>
    <h1>Project {{ route.params?.slug }}</h1>
  </div>
</template>
