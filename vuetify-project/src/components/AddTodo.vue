<template>
  <v-text-field :value="newTodo" @input="$emit('update:newTodo', $event.target.value)" @keyup.enter="addTodo"
    label="Add a new task" solo></v-text-field>
</template>

<script>
export default {
  props: {
    newTodo: String
  },
  methods: {
    addTodo() {
      this.$emit('add-todo', this.newTodo);
    }
  }
};
</script>
