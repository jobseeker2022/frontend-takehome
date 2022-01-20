<script>
import { ref } from "vue";
import HeaderVue from "./components/Header.vue";
export default {
  components: { HeaderVue },
  setup() {
    const count = ref(0);

    function increment(number) {
      count.value = count.value + 1;
    }

    function reset() {
      count.value = 0;
    }

    return { count, increment, reset };
  },
};
</script>

<template>
  <div id="app">
    <header-vue />
    <h1 class="title">Hello, world!</h1>
    <p>The count is {{ count }}.</p>
    <button @click="increment">Increment count</button>
    <button @click="reset">Reset count</button>
  </div>
</template>

<style></style>
