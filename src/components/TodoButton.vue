<script setup></script>
<template>
  <button><slot>Default</slot></button>
</template>

<style lang="scss" scoped>
button {
  cursor: pointer;
  background-color: aliceblue;
  border: none;
  padding: 0 14px;
  transition: all 250ms ease;
  &:hover {
    background-color: rgb(178, 218, 253);
  }
}
</style>
