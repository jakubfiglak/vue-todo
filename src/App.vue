<template>
  <div id="app">
    <Header @theme-toggle="toggleTheme" :theme="userTheme" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Header from './components/Header.vue';
import { Theme } from './types';

type Data = {
  userTheme: Theme;
};

export default Vue.extend({
  name: 'App',
  components: {
    Header,
  },
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
  -webkit-font-smoothing: antialiased;
  font-size: 1.8rem;
  font-family: 'Josefin Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Open Sans',
    'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: var(--body-background);
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

:root {
  --bright-blue: hsl(220, 98%, 61%);
  --check-background: linear-gradient hsl(192, 100%, 67%) to hsl(280, 87%, 65%);
  --todo-background: hsl(0, 0%, 98%);
  --body-background: hsl(236, 33%, 92%);
  --light-grayish-blue: hsl(233, 11%, 84%);
  --dark-grayish-blue: hsl(236, 9%, 61%);
  --very-dark-grayish-blue: hsl(235, 19%, 35%);
  --heading-color: hsl(0, 0%, 100%);
  --desktop-header-background: url('./assets/bg-desktop-light.jpg');
  --mobile-header-background: url('./assets/bg-mobile-light.jpg');
}

:root.dark-theme {
  --body-background: hsl(235, 21%, 11%);
  --todo-background: hsl(235, 24%, 19%);
  --light-grayish-blue: hsl(234, 39%, 85%);
  --light-grayish-blue-hover: hsl(236, 33%, 92%);
  --dark-grayish-blue: hsl(234, 11%, 52%);
  --very-dark-grayish-blue: hsl(233, 14%, 35%);
  --very-dark-grayish-blue-hover: hsl(237, 14%, 26%);
  --desktop-header-background: url('./assets/bg-desktop-dark.jpg');
  --mobile-header-background: url('./assets/bg-mobile-dark.jpg');
}
</style>
