<template>
  <section>
    <todo-form @add-todo="addTodo" />
    <todo-list :todos="todos" @toggle-completed="toggleCompleted" @delete-todo="deleteTodo" />
  </section>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';
import { Todo } from '../types';

export default Vue.extend({
  name: 'Todos',
  components: { TodoForm, TodoList },
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
      default: [],
    },
  },
  methods: {
    toggleCompleted({ completed, id }: { completed: boolean; id: string }) {
      this.$emit('toggle-completed', { completed, id });
    },
    deleteTodo(id: string) {
      this.$emit('delete-todo', id);
    },
    addTodo({ completed, text }: { completed: boolean; text: string }) {
      this.$emit('add-todo', { completed, text });
    },
  },
});
</script>

<style scoped>
section {
  margin-top: -9.2rem;
}
</style>
