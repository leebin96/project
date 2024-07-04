<template>
  <v-text-field v-model="localSearch" @input="updateSearch" label="Search tasks" solo></v-text-field>
</template>

<script>
export default {
  props: {
    value: String
  },
  data() {
    return {
      localSearch: this.value
    };
  },
  methods: {
    updateSearch(event) {
      this.localSearch = event.target.value;
      this.$emit('update:modelValue', this.localSearch);
    }
  },
  watch: {
    value(newValue) {
      this.localSearch = newValue;
    }
  }
};
</script>
