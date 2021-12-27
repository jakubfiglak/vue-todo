<template>
  <div class="item">
    <checkbox
      name="completed"
      :checked="completed"
      @input="$emit('toggle-completed', { completed: !completed, id })"
    />
    <span :class="{ 'is-complete': completed }">{{ text }}</span>
    <button @click="$emit('delete-todo', id)">
      <InlineSvg :src="require('../assets/icon-cross.svg')" />
    </button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import InlineSvg from 'vue-inline-svg';
import Checkbox from './Checkbox.vue';

export default Vue.extend({
  name: 'TodoItem',
  components: { Checkbox, InlineSvg },
  props: {
    id: {
      type: String,
      required: true,
    },
    completed: {
      type: Boolean,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
  },
});
</script>

<style scoped>
.item {
  display: flex;
  align-items: center;
  padding: 1.6rem 2rem;
  border-bottom: 1px solid var(--very-dark-grayish-blue-hover);
}

span {
  margin-left: 1.6rem;
}

.is-complete {
  color: var(--light-text-color);
  text-decoration: line-through;
}

button {
  margin-left: auto;
  border: 0;
  background: none;
  cursor: pointer;
}
</style>
