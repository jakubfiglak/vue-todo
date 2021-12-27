<template>
  <header>
    <LayoutContentWrapper>
      <div class="container">
        <h1>todo</h1>
        <button @click="$emit('theme-toggle')">
          <InlineSvg v-if="theme === 'dark-theme'" :src="require('../assets/icon-sun.svg')" />
          <InlineSvg v-else :src="require('../assets/icon-moon.svg')" />
        </button>
      </div>
    </LayoutContentWrapper>
  </header>
</template>

<script lang="ts">
import Vue from 'vue';
import InlineSvg from 'vue-inline-svg';
import LayoutContentWrapper from './LayoutContentWrapper.vue';
import { Theme } from '../types';

export default Vue.extend({
  name: 'Header',
  components: { LayoutContentWrapper, InlineSvg },
  props: {
    theme: String as () => Theme,
  },
});
</script>

<style scoped>
header {
  height: 200px;
  background-image: var(--mobile-header-background);
  background-size: cover;
  background-repeat: no-repeat;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 4.8rem;
}

h1 {
  color: var(--heading-color);
  font-size: 2rem;
  letter-spacing: 1rem;
  text-transform: uppercase;
}

button {
  border: 0;
  background: none;
  cursor: pointer;
}

@media screen and (min-width: 500px) {
  header {
    height: 300px;
    background-image: var(--desktop-header-background);
  }

  h1 {
    font-size: 4rem;
  }
}
</style>
