<template>
  <v-container>
    <h1>ToDo List</h1>
    <v-text-field v-model="newTodo" @keyup.enter="addTodo" label="Add a new task" solo></v-text-field>
    <v-text-field v-model="search" @input="filterTodos" label="Search tasks" solo></v-text-field>
    <v-list>
      <v-list-item v-for="(todo, index) in filteredTodos" :key="index">
        <v-list-item-content>
          <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        </v-list-item-content>
        <v-list-item-action>
          <v-btn icon @click="toggleComplete(index)">
            <v-icon>{{ todo.completed ? 'mdi-checkbox-marked' : 'mdi-checkbox-blank-outline' }}</v-icon>
          </v-btn>
          <v-btn icon @click="removeTodo(index)">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
      </v-list-item>
    </v-list>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      search: ''
    };
  },
  computed: {
    filteredTodos() {
      if (!this.search.trim()) {
        return this.todos;
      }
      const searchTerm = this.search.trim().toLowerCase();
      return this.todos.filter(todo =>
        todo.text.toLowerCase().includes(searchTerm)
      );
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({
          text: this.newTodo.trim(),
          completed: false
        });
        this.saveTodos(); // 추가한 할일을 저장
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
      this.saveTodos(); // 할일을 삭제한 후 저장
    },
    toggleComplete(index) {
      this.todos[index].completed = !this.todos[index].completed;
      this.saveTodos(); // 할일 상태 변경 후 저장
    },
    filterTodos() {
      // 필터링은 computed 속성인 filteredTodos를 통해 자동으로 처리됨
    },
    saveTodos() {
      // 필요한 경우에만 각 할일 항목을 최소화하여 저장
      const minimalTodos = this.todos.map(todo => ({
        text: todo.text,
        completed: todo.completed
      }));
      localStorage.setItem('todos', JSON.stringify(minimalTodos));
    },
    loadTodos() {
      const savedTodos = localStorage.getItem('todos');
      this.todos = savedTodos ? JSON.parse(savedTodos) : [];
    }
  },
  created() {
    this.loadTodos(); // 페이지가 생성될 때 저장된 할일 목록을 불러옴
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
