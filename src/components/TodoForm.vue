<template>
  <layout-content-wrapper>
    <form @submit.prevent="addTodo">
      <fieldset>
        <checkbox name="completed" :checked="completed" v-model="completed" />
        <input type="text" name="text" id="text" placeholder="Create new todo..." v-model="text" />
      </fieldset>
    </form>
  </layout-content-wrapper>
</template>

<script lang="ts">
import Vue from 'vue';
import LayoutContentWrapper from './LayoutContentWrapper.vue';
import Checkbox from './Checkbox.vue';

export default Vue.extend({
  name: 'TodoForm',
  components: { LayoutContentWrapper, Checkbox },
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

input[type='text'] {
  background: none;
  border: 0;
  color: var(--text-color);
  margin-left: 1.2rem;
}
</style>
