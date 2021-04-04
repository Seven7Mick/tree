<template>
  <div id="app">
    <Tree class="app_tree" />
  </div>
</template>

<script>
import Tree from "@/components/Tree.vue";

export default {
  name: "App",
  components: {
    Tree,
  },
};
</script>

<style>
#app {
  font-family: 'Segoe UI', Tahoma, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: Tahoma, sans-serif;
}

li {
  list-style: none;
}

.app_tree {
  margin-top: 10px;
}

button {
  border: none;
  background: none;
  cursor: pointer;
}
</style>
