<template>
  <TodoList />
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>

<style lang="scss">
body {
  background-color: rgb(43, 43, 43);
}
</style>
