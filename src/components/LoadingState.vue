<template>
<div class="container">
  <div class="loading-dots m-auto pt-6" />
</div>
</template>

<style scoped>
  .container {
    height: 50vh;
    width: 50vw;
  }
  .loading-dots {
    width: 235px;
    height: 35px;
    background: radial-gradient(circle closest-side,currentColor 90%,#0000) 0 0/33% 100% space;
    clip-path: inset(0 100% 0 0);
    animation: move 1s steps(4) infinite;
  }
  @keyframes move {
    to {
      clip-path: inset(0 -34% 0 0)
    }
  }
</style>