<script setup lang="ts">
import { RouterLink } from "vue-router";
import { supabase } from "@/lib/supabaseClient";
import { ref } from "vue";
import type { Tables } from "../../../database/types";

const projects = ref<Tables<"projects">[] | null>(null);

(async () => {
  //imediately invoked function
  const { data, error } = await supabase.from("projects").select();

  if (error) console.log(error);

  projects.value = data;
})();
</script>

<template>
  <div>
    <h1 class="text-yellow-600">Projects Page</h1>
    <RouterLink to="/">Go To Home</RouterLink>
    <RouterLink :to="{ name: '/projects/[id]', params: { id: 1 } }"
      >Go To Project with id</RouterLink
    >
    <ul>
      <li v-for="project in projects" :key="project.id">
        {{ project.name }}
      </li>
    </ul>
  </div>
</template>
