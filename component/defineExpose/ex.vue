<template>
  <div>
    <h3>Custom: {{ customLoading }}</h3>
    <h3>State: {{ state.isLoading }}</h3>
    <ul :style="{background: state.isLoading ? 'gray' : 'white'}">
      <li v-for="todo in todos" :key="todo.id">
        {{ todo.title }}
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  customLoading: {
    type: Boolean,
    default: false
  }
});
const state = reactive({
  isLoading: !!props.customLoading
})
interface Todo {
  [key: string]: any
}
const todos: Todo = ref([{ id: 1, title: 'Todo 1', completed: true }]);
const fetchData = () => {
  state.isLoading = true
  todos.value = [
    { id: 1, title: 'Todo 1', completed: true },
    { id: 2, title: 'Todo 2', completed: true },
    { id: 3, title: 'Todo 3', completed: true },
    { id: 4, title: 'Todo 4', completed: true }
  ]
  setTimeout(() => {
    state.isLoading = false
  }, 2000);
}
watchEffect(() => {
  fetchData();
});
const reset = () => {
  state.isLoading = true;
  setTimeout(() => {
    todos.value = [{ id: 1, title: 'Todo 1', completed: true }];
    state.isLoading = false;
  }, 5000);
}
defineExpose({
  fetchData,
  todos,
  reset,
  state
});
</script>
