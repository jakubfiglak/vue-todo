<template>
  <layout-content-wrapper>
    <form @submit.prevent="addTodo">
      <fieldset>
        <input type="checkbox" name="completed" id="completed" v-model="completed" />
        <input type="text" name="text" id="text" placeholder="Create new todo..." v-model="text" />
      </fieldset>
    </form>
  </layout-content-wrapper>
</template>

<script lang="ts">
import Vue from 'vue';
import LayoutContentWrapper from './LayoutContentWrapper.vue';

export default Vue.extend({
  name: 'TodoForm',
  components: { LayoutContentWrapper },
  data() {
    return {
      completed: false,
      text: '',
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        completed: this.completed,
        text: this.text,
      };
      this.$emit('add-todo', newTodo);
      this.completed = false;
      this.text = '';
    },
  },
});
</script>

<style scoped>
fieldset {
  background: var(--todo-background);
  border: 0;
  display: flex;
  align-items: center;
  padding: 1.8rem 2rem;
  box-shadow: var(--box-shadow);
  border-radius: var(--border-radius);
}

input[type='checkbox'] {
  cursor: pointer;
  appearance: none;
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  border: 1px solid var(--very-dark-grayish-blue);
}

input[type='checkbox']:checked {
  background: url(../assets/icon-check.svg) no-repeat center, var(--check-background);
}

input[type='text'] {
  background: none;
  border: 0;
  color: var(--text-color);
  margin-left: 1.2rem;
}
</style>
