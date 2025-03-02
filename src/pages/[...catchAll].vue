<script setup lang="ts">
import { usePageStore } from '@/stores/page';

usePageStore().pageData.title = '404 Error'
</script>

<template>
    <div>
        <h1 class="text-red-600">
            404 Not Found !!
        </h1>
    </div>
</template>