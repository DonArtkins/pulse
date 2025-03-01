<script setup lang="ts">
import { RouterLink } from "vue-router";
import { supabase } from "@/lib/supabaseClient";
import { ref } from "vue";
import type { Tables } from "../../../database/types";

const tasks = ref<Tables<"tasks">[] | null>(null);

(async () => {
  //imediately invoked function
  const { data, error } = await supabase.from("tasks").select();

  if (error) console.log(error);

  tasks.value = data;
})();
</script>

<template>
    <div>
    <h1 class="text-purple-600">Tasks Page</h1>
    <RouterLink to="/">Go To Home</RouterLink>
    <RouterLink :to="{ name: '/tasks/[id]', params: { id: 1 } }"
      >Go To Task with id</RouterLink
    >
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{ task.name }}
      </li>
    </ul>
  </div>
</template>