<script setup lang="ts">
import { RouterLink } from "vue-router";
import { h, ref } from "vue";
import type { ColumnDef } from "@tanstack/vue-table";
import {
  tasksWithProjectsQuery,
  type TasksWithProjects,
} from "@/utils/superQueries";

const tasks = ref<TasksWithProjects | null>(null);

const getTasks = async () => {
  const { data, error } = await tasksWithProjectsQuery;

  if (error) console.log(error);

  tasks.value = data;
};

await getTasks();

const columns: ColumnDef<TasksWithProjects[0]>[] = [
  {
    accessorKey: "name",
    header: () => h("div", { class: "text-left" }, "Name"),
    cell: ({ row }) => {
      /**
       * The `h` tag is a vue fuction that returns html elements and it accepts 3 arguments (string to rep tag name or component instance, object that has properties for the attributes and finally the last argument and whatever is passed to it will be placed inside the element)
       */
      return h(
        RouterLink,
        {
          to: `/tasks/${row.original.id}`,
          class: "text-left font-medium hover:bg-muted",
        },
        () => row.getValue("name")
      );
    },
  },
  {
    accessorKey: "status",
    header: () => h("div", { class: "text-left" }, "Status"),
    cell: ({ row }) => {
      return h(
        "div",
        { class: "text-left font-medium" },
        row.getValue("status")
      );
    },
  },
  {
    accessorKey: "due_date",
    header: () => h("div", { class: "text-left" }, "Due Date"),
    cell: ({ row }) => {
      return h(
        "div",
        { class: "text-left font-medium" },
        row.getValue("due_date")
      );
    },
  },
  {
    accessorKey: "projects",
    header: () => h("div", { class: "text-left" }, "Project"),
    cell: ({ row }) => {
      return row.original.projects
        ? h(
            RouterLink,
            {
              to: `/projects/${row.original.projects.slug}`,
              class: "text-left font-medium hover:bg-muted",
            },
            () => row.original.projects?.name
          )
        : "";
    },
  },
  {
    accessorKey: "collaborators",
    header: () => h("div", { class: "text-left" }, "Collaborators"),
    cell: ({ row }) => {
      return h(
        "div",
        { class: "text-left font-medium" },
        JSON.stringify(row.getValue("collaborators"))
      );
    },
  },
];
</script>

<template>
  <DataTable v-if="tasks" :columns="columns" :data="tasks" />
</template>
