<template>
  <div id="app">
    <HeaderList />
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import HeaderList from "./components/HeaderList.vue";

export default {
  name: "App",
  components: {
    TodoList,
    HeaderList,
  },
};
</script>

<style>
#app {
}
</style>
