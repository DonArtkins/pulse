<script setup lang="ts">
import { RouterLink } from "vue-router";
import { supabase } from "@/lib/supabaseClient";
import { h, ref } from "vue";
import type { Tables } from "../../../database/types";
import type { ColumnDef } from "@tanstack/vue-table";
import { DataTable } from "@/components";

const tasks = ref<Tables<"tasks">[] | null>(null);

(async () => {
  //imediately invoked function
  const { data, error } = await supabase.from("tasks").select();

  if (error) console.log(error);

  tasks.value = data;
})();

const columns: ColumnDef<Tables<"tasks">>[] = [
  {
    accessorKey: "name",
    header: () => h("div", { class: "text-left" }, "Name"),
    cell: ({ row }) => {
      /**
       * The `h` tag is a vue fuction that returns html elements and it accepts 3 arguments (string to rep tag name or component instance, object that has properties for the attributes and finally the last argument and whatever is passed to it will be placed inside the element)
       */
      return h("div", { class: "text-left font-medium" }, row.getValue("name"));
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
    accessorKey: "due_date",
    header: () => h("div", { class: "text-left" }, "Due Date"),
    cell: ({ row }) => {
      return h("div", { class: "text-left font-medium" }, row.getValue("due_date"));
    },
  },
  {
    accessorKey: "project_id",
    header: () => h("div", { class: "text-left" }, "Project Id"),
    cell: ({ row }) => {
      return h("div", { class: "text-left font-medium" }, row.getValue("project_id"));
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
  <DataTable v-if="tasks" :columns="columns" :data="tasks" />
</template>
