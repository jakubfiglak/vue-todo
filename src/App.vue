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
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;700&display=swap');

*,
*::before,
*::after {
  box-sizing: border-box;
}

* {
  margin: 0;
}

html,
body {
  height: 100%;
}

html {
  font-size: 62.5%;
  width: 100%;
  overflow-y: scroll;
}

body {
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  font-size: 1.8rem;
}

img,
picture,
video,
canvas,
svg {
  display: block;
  max-width: 100%;
}

input,
button,
textarea,
select {
  font: inherit;
}

p,
h1,
h2,
h3,
h4,
h5,
h6 {
  overflow-wrap: break-word;
}

#app {
  font-family: 'Josefin Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Open Sans',
    'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: var(--background-color);
}

:root {
  --background-color: white;
}

:root.dark-theme {
  --background-color: black;
}
</style>
