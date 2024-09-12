<template>
  <div class="nav-container">
    <span class="title">{{ simName }}</span>
    <nav>
      <a class="nav-link" href="#">Conceitos de programação</a>
    </nav>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    simName: { type: String, required: true },
  },
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

nav {
  margin-right: 0.5rem;
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

.nav-link:hover {
  background-color: #69b7da;
  border-radius: 1rem;
}
</style>
