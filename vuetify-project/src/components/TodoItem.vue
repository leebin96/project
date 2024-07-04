<template>
  <v-list-item @click="toggleComplete(todo)" :class="{ completed: todo.completed }">
    <v-list-item-content>
      {{ todo.text }}
      <span v-if="todo.completed" class="completed-label"> (완료)</span>
    </v-list-item-content>
    <v-list-item-action>
      <v-btn icon @click.stop="removeTodo">
        <v-icon>mdi-delete</v-icon>
      </v-btn>
    </v-list-item-action>
  </v-list-item>
</template>

<script>
export default {
  props: {
    todo: Object,
    index: Number
  },
  methods: {
    toggleComplete(todo) {
      this.$emit('toggle-complete', todo);
    },
    removeTodo() {
      this.$emit('remove-todo', this.index);
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: gray;
}
.completed-label {
  color: green;
  font-weight: bold;
}
</style>
