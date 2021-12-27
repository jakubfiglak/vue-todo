<template>
  <input
    type="checkbox"
    :name="name"
    :checked="checked"
    @input="$emit('input', $event.target.checked)"
  />
</template>

<script lang="ts">
export default {
  name: 'Checkbox',
  props: {
    name: {
      type: String,
      required: true,
    },
    checked: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
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
</style>
