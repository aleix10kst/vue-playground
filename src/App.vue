<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "@vue/reactivity";
import TodoList from "./components/TodoList.vue";
import { Todo } from "./lib/models/todo.type";
import Header from "./components/Header.vue";

const todos = ref<Todo[]>([
  {
    id: 1,
    title: "Aprendre Python",
    description: "",
    createdAt: new Date(),
  },
  {
    id: 2,
    title: "Aprendre Javascript",
    description: "Hello",
    createdAt: new Date(),
  },
]);

const selectedTodo = ref<Todo | null>(null);

const onAddTodo = () => {
  todos.value = [
    ...todos.value,
    { id: 3, title: "Angular", description: "", createdAt: new Date() },
  ];
};

const onCompleteTodo = (id: number) =>
  (todos.value = todos.value.map((todo) =>
    todo.id === id
      ? { ...todo, completed: !todo.completed, updatedAt: new Date() }
      : todo
  ));

const onEditTodo = (todoId: number) => {
  const index = todos.value.findIndex(({ id }) => id === todoId);
  console.log(index, todoId);
  if (index !== -1) selectedTodo.value = todos.value[index];
};
const onRemoveTodo = (id: number) =>
  (todos.value = todos.value.filter((todo) => todo.id !== id));
</script>

<template>
  <div class="bg-white min-h-screen px-2 md:px-0">
    <div class="max-w-7xl mx-auto">
      <Header class="mb-4" />
      <main>
        <TodoList
          :todos="todos"
          @add-todo="onAddTodo"
          @complete-todo="onCompleteTodo"
          @edit-todo="onEditTodo"
          @remove-todo="onRemoveTodo"
          class="mb-4"
        />
        <template v-if="selectedTodo">
          Todo seleccionat: {{ JSON.stringify(selectedTodo) }}
        </template>
      </main>
    </div>
  </div>
</template>

<style></style>
