<script setup lang="ts">
import AdviceCard from "./components/AdviceCard.vue"
</script>

<template>
  <main>
    <advice-card />
  </main>
</template>

<style>
body {
  display: grid;
  place-items: center;
  min-height: 100vh;
  overflow: hidden;
  background-color: hsl(218, 23%, 16%);
  font-family: "Manrope", sans-serif;
}
</style>
