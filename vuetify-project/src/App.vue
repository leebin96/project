<template>
  <v-app>
    <TodoList />
  </v-app>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList
  }
};
</script>

<style>
/* 글로벌 스타일을 추가할 수 있습니다. */
</style>
