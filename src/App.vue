<template>
  <TodoList />
  <TwoCom />
</template>

<script>
import TodoList from "./components/TodoList.vue";
import TwoCom from "./components/TwoCom.vue";

export default {
  name: "App",
  components: {
    TodoList,
    TwoCom,
  },
};
</script>

<style lang="scss">
body {
  background-color: rgb(83, 83, 83);
}
</style>
