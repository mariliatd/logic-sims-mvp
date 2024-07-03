<template>
  <div class="nav-container">
    <span class="title">{{ simName }}</span>
    <nav>
      <a class="nav-link" href="#">Ajuda</a>
    </nav>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  simName: { type: String, required: true },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Fuzzy+Bubbles:wght@400;700&display=swap");

body {
  margin: 0;
}

a {
  text-decoration: none;
  color: inherit;
}

.title {
  font-family: "Fuzzy Bubbles", sans-serif;
  font-size: 2rem;
  color: #1d2d44;
  padding: 0.5rem 1rem;
}

.nav-container {
  background-color: #86c5e1;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-link {
  padding: 0.5rem 1rem;
}
</style>
