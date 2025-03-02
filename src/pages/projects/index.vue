<script setup lang="ts">
import { RouterLink } from "vue-router";
import { supabase } from "@/lib/supabaseClient";
import { h, ref } from "vue";
import type { Tables } from "../../../database/types";
import type { ColumnDef } from "@tanstack/vue-table";
import { DataTable } from "@/components";

const projects = ref<Tables<"projects">[] | null>(null);

(async () => {
  //imediately invoked function
  const { data, error } = await supabase.from("projects").select();

  if (error) console.log(error);

  projects.value = data;
})();

const columns: ColumnDef<Tables<"projects">>[] = [
  {
    accessorKey: "name",
    header: () => h("div", { class: "text-left" }, "Name"),
    cell: ({ row }) => {
      /**
       * The `h` tag is a vue fuction that returns html elements and it accepts 3 arguments (string to rep tag name or component instance, object that has properties for the attributes and finally the last argument and whatever is passed to it will be placed inside the element)
       */
      return h(RouterLink, { to:`/projects/${ row.original.slug }`, class: "text-left font-medium hover:bg-muted block w-full" }, () => row.getValue("name"));
    },
  },
  {
    accessorKey: "slug",
    header: () => h("div", { class: "text-left" }, "Slug"),
    cell: ({ row }) => {
      return h("div", { class: "text-left font-medium" }, row.getValue("slug"));
    },
  },
  {
    accessorKey: "status",
    header: () => h("div", { class: "text-left" }, "Status"),
    cell: ({ row }) => {
      return h("div", { class: "text-left font-medium" }, row.getValue("status"));
    },
  },
  {
    accessorKey: "collaborators",
    header: () => h("div", { class: "text-left" }, "Collaborators"),
    cell: ({ row }) => {
      return h("div", { class: "text-left font-medium" }, JSON.stringify(row.getValue("collaborators")));
    },
  },
];
</script>

<template>
  <DataTable v-if="projects" :columns="columns" :data="projects" />
</template>
