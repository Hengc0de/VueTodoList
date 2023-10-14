<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <header>
    <nav class="container">
      <div class="branding">
        <img src="../assets/Microsoft_To-Do_icon.png" alt="" />
        <h1>Vue Todo</h1>
      </div>
      <ul class="nav-routes">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped>
header {
  background-color: #f1f1f1;
  nav {
    display: flex;
    justify-content: center;
    padding: 16px 32px;
    .branding {
      gap: 10px;
      align-items: center;
      display: flex;
      justify-content: center;
      img {
        width: 48px;
      }
      h1 {
        font-size: 24px;
      }
    }
    .nav-routes {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 12px;
      flex: 1;
      list-style: none;
      a {
        text-decoration: none;
        color: inherit;
      }
    }
  }
}
</style>
