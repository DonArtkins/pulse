<script setup lang="ts">
import { RouterView } from "vue-router";
import { supabase } from "@/lib/supabaseClient";
import { AuthLayout } from "@/components";
</script>

<template>
  <AuthLayout>
    <RouterView />
  </AuthLayout>
</template>
