<script>
import { ref } from "vue";
export default {
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
    <h1 class="title">Hello, world!</h1>
    <p>The count is {{ count }}.</p>
    <button @click="increment">Increment count</button>
    <button @click="reset">Reset count</button>
  </div>
</template>

<style></style>
