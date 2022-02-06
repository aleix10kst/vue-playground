<script setup lang="ts">
import { Todo } from "../lib/models/todo.type";
import { CheckCircleIcon, XCircleIcon, PencilIcon } from "@heroicons/vue/solid";

const props = defineProps<{ todo: Todo }>();

defineEmits<{
  complete: (id: number) => void;
  remove: (id: number) => void;
  edit: (id: number) => void;
}>();

const formatDate = (date: Date) =>
  new Intl.DateTimeFormat("es-ES").format(date);
</script>

<template>
  <div
    class="flex flex-col min-h-content border border-gray-200 px-2 py-3 rounded-lg shadow-lg"
  >
    <div class="flex justify-between">
      <h3 class="text-gray-800 text-lg font-bold mb-0.5">{{ todo.title }}</h3>
      <button
        class="rounded-full border border-yellow-600 hover:bg-yellow-100 w-8 h-8"
        @click="$emit('edit', todo.id)"
      >
        <PencilIcon class="text-yellow-600 font-bold m-auto w-4 h-4" />
      </button>
    </div>
    <p class="text-sm text-gray-500">
      Creat el:
      <span class="font-semibold">{{ formatDate(todo.createdAt) }}</span>
      <template v-if="todo.updatedAt">
        - Actualitzat el
        <span class="font-semibold">{{
          formatDate(todo.updatedAt)
        }}</span></template
      >
    </p>
    <p class="mb-2 text-sm text-gray-500 flex">
      Estat:
      <CheckCircleIcon
        class="inline-block h-5 w-5 text-green-900 align-middle ml-1"
        v-if="todo.completed"
      />
      <XCircleIcon
        class="inline-block h-5 w-5 text-red-900 align-middle ml-1"
        v-if="!todo.completed"
      />
    </p>
    <p class="text-gray-700 mb-4">{{ todo.description }}</p>
    <div class="mt-auto flex flex-col space-y-2">
      <button
        type="button"
        class="inline-flex justify-center px-4 py-2 text-sm font-medium text-green-900 bg-green-100 border border-transparent rounded-md hover:bg-green-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 focus-visible:ring-green-500"
        @click="$emit('complete', todo.id)"
      >
        Completa
      </button>
      <button
        type="button"
        class="inline-flex justify-center px-4 py-2 text-sm font-medium text-red-900 bg-red-100 border border-transparent rounded-md hover:bg-red-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 focus-visible:ring-red-500"
        @click="$emit('remove', todo.id)"
      >
        Esborra
      </button>
    </div>
  </div>
</template>

<style></style>
