<script setup lang="ts">
import { Todo } from "../lib/models/todo.type";
import TodoItem from "./TodoItem.vue";

defineProps<{ todos: Todo[] }>();
defineEmits<{
  addTodo: () => void;
  completeTodo: (id: number) => void;
  editTodo: (id: number) => void;
  removeTodo: (id: number) => void;
}>();
</script>

<template>
  <section class="space-y-4">
    <div class="flex justify-between">
      <h2 class="text-3xl font-bold text-stone-700">List of todos</h2>
      <button
        type="button"
        class="inline-flex justify-center px-4 py-2 text-sm font-medium text-blue-900 bg-blue-100 border border-transparent rounded-md hover:bg-blue-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 focus-visible:ring-blue-500"
        @click="$emit('addTodo')"
      >
        Afegeix tasca
      </button>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <TodoItem
        v-for="(todo, idx) in todos"
        :key="idx"
        :todo="todo"
        @complete="$emit('completeTodo', $event)"
        @edit="$emit('editTodo', $event)"
        @remove="$emit('removeTodo', $event)"
      ></TodoItem>
    </div>
  </section>
</template>

<style></style>
