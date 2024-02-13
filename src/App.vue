<template>
  <AppHeader />

  <AppFilters />

  <main class="app-main">
    <AppTodoList
      :todos="todos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />

    <AppAddTodo @add-todo="addTodo" />
  </main>

  <AppFooter />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFooter from "./components/AppFooter.vue";
import { Todo } from "./types/Todo";

interface State {
  todos: Todo[];
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter,
  },
  data(): State {
    return {
      todos: [
        { id: 0, text: "Learn the basics of Vue", complited: true },
        { id: 1, text: "Learn the basics of Typescript", complited: false },
        { id: 2, text: "Subscribe to the channel", complited: false },
        // { id: '3', stext: 'Todoitem' },
      ],
    };
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);

      if (targetTodo) {
        targetTodo.complited = !targetTodo.complited;
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
    },
  },
});
</script>
