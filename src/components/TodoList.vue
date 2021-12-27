<template>
  <layout-content-wrapper>
    <div class="container">
      <todo-item
        v-for="todo in todos"
        :key="todo.id"
        :id="todo.id"
        :completed="todo.completed"
        :text="todo.text"
        @toggle-completed="toggleCompleted"
        @delete-todo="deleteTodo"
      />
    </div>
  </layout-content-wrapper>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';
import TodoItem from './TodoItem.vue';
import LayoutContentWrapper from './LayoutContentWrapper.vue';
import { Todo } from '../types';

export default Vue.extend({
  components: { TodoItem, LayoutContentWrapper },
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
  },
});
</script>

<style scoped>
.container {
  margin-top: 1.6rem;
  background: var(--todo-background);
  color: var(--text-color);
  border-radius: var(--border-radius);
}
</style>
