<template>
  <section>
    <todo-form />
  </section>
</template>

<script>
import Vue from 'vue';
import TodoForm from './TodoForm.vue';

export default Vue.extend({
  name: 'Todos',
  components: { TodoForm },
});
</script>

<style scoped>
section {
  margin-top: -9.2rem;
}
</style>
