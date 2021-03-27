<template>
  <div id="app" class="max-w-screen-md mx-auto bg-gray-50">
    <list-products />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ListProducts from "./components/ListProducts.vue";

export default defineComponent({
  name: "App",
  components: {
    ListProducts,
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
}
</style>
