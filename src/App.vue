<template>
  <div id="app">
    <Header @theme-toggle="toggleTheme" :theme="userTheme" />
    <todos
      :todos="todos"
      @toggle-completed="toggleCompleted"
      @delete-todo="deleteTodo"
      @add-todo="addTodo"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { v4 as uuidv4 } from 'uuid';
import Header from './components/Header.vue';
import Todos from './components/Todos.vue';
import { Theme, Todo } from './types';

type Data = {
  userTheme: Theme;
  todos: Todo[];
};

export default Vue.extend({
  name: 'App',
  components: {
    Header,
    Todos,
  },
  mounted() {
    const initUserTheme = this.getMediaPreference();
    this.setTheme(initUserTheme);
  },
  data(): Data {
    return {
      userTheme: 'light-theme',
      todos: [
        {
          id: '1',
          completed: true,
          text: 'Complete online JavaScript course',
        },
        {
          id: '2',
          completed: false,
          text: 'Jog around the park 3x',
        },
        {
          id: '3',
          completed: false,
          text: '10 minutes meditation',
        },
        {
          id: '4',
          completed: false,
          text: 'Read for 1 hour',
        },
        {
          id: '5',
          completed: false,
          text: 'Pick up groceries',
        },
        {
          id: '6',
          completed: false,
          text: 'Complete Todo App on Frontend Mentor',
        },
      ],
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
    toggleCompleted({ completed, id }: { completed: boolean; id: string }) {
      const todoIndex = this.todos.findIndex((t) => t.id === id);
      this.todos[todoIndex].completed = completed;
    },
    deleteTodo(id: string) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo({ completed, text }: { completed: boolean; text: string }) {
      const newTodo = {
        id: uuidv4(),
        completed,
        text,
      };
      this.todos = [newTodo, ...this.todos];
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
  --check-background: linear-gradient(hsl(192, 100%, 67%), hsl(280, 87%, 65%));
  --todo-background: hsl(0, 0%, 98%);
  --body-background: hsl(236, 33%, 92%);
  --light-grayish-blue: hsl(233, 11%, 84%);
  --dark-grayish-blue: hsl(236, 9%, 61%);
  --very-dark-grayish-blue: hsl(235, 19%, 35%);
  --very-dark-grayish-blue-hover: hsl(237, 14%, 26%);
  --text-color: var(--very-dark-grayish-blue);
  --light-text-color: var(--dark-grayish-blue);
  --heading-color: hsl(0, 0%, 100%);
  --desktop-header-background: url('./assets/bg-desktop-light.jpg');
  --mobile-header-background: url('./assets/bg-mobile-light.jpg');
  --box-shadow: 0px 35px 50px -15px rgba(194, 195, 214, 0.5);
  --border-radius: 5px;
}

:root.dark-theme {
  --body-background: hsl(235, 21%, 11%);
  --todo-background: hsl(235, 24%, 19%);
  --text-color: hsl(234, 39%, 85%);
  --light-text-color: hsl(235, 16%, 43%);
  --light-grayish-blue: hsl(234, 39%, 85%);
  --light-grayish-blue-hover: hsl(236, 33%, 92%);
  --dark-grayish-blue: hsl(234, 11%, 52%);
  --very-dark-grayish-blue: hsl(233, 14%, 35%);
  --desktop-header-background: url('./assets/bg-desktop-dark.jpg');
  --mobile-header-background: url('./assets/bg-mobile-dark.jpg');
}
</style>
