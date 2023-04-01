<script setup>
import { RouterLink } from "vue-router";
</script>
<template>
  <header class="container">
    <div class="branding">
      <img src="../assets/Vue_Logo_Black.png" alt="Vue image" />
      <h1>Vue Todo</h1>
    </div>
    <nav>
      <RouterLink to="/">Todos</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
header {
  background-color: #f1f1f1;
  display: flex;
  align-items: center;
  padding: 25px 16px;
  .branding {
    display: flex;
    align-items: center;
    gap: 8px;
    img {
      max-width: 50px;
    }
    h1 {
      font-size: 24px;
    }
  }
  nav {
    display: flex;
    flex: 1;
    justify-content: flex-end;
    gap: 12px;
    a {
      text-decoration: none;
      color: inherit;
    }
  }
}
</style>
