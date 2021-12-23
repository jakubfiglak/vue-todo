<template>
  <div id="app">
    <h1>Hello</h1>
    <button @click="toggleTheme">Toggle Theme</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

type Theme = 'light-theme' | 'dark-theme';
type Data = {
  userTheme: Theme;
};

export default Vue.extend({
  name: 'App',
  mounted() {
    const initUserTheme = this.getMediaPreference();
    this.setTheme(initUserTheme);
  },
  data(): Data {
    return {
      userTheme: 'light-theme',
    };
  },
  methods: {
    setTheme(theme: Theme) {
      localStorage.setItem('user-theme', theme);
      this.userTheme = theme;
      document.documentElement.className = theme;
    },
    toggleTheme() {
      const activeTheme = localStorage.getItem('user-theme') as Theme | undefined;
      if (activeTheme === 'light-theme') {
        this.setTheme('dark-theme');
      } else {
        this.setTheme('light-theme');
      }
    },
    getMediaPreference(): Theme {
      const hasDarkPreference = window.matchMedia('(prefers-color-scheme: dark)').matches;

      if (hasDarkPreference) {
        return 'dark-theme';
      }
      return 'light-theme';
    },
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: var(--background-color);
}

:root {
  --background-color: white;
}

:root.dark-theme {
  --background-color: black;
}
</style>
