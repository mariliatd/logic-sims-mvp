<template>
  <div class="counter-box">
    <p class="label-text">{{ label }}</p>
    <div class="counter">
      <v-btn
        variant="text"
        style="min-width: 0; left: 0.5rem; margin-right: 0.5rem; padding: 0"
        @click="count++"
      >
        <v-icon icon="mdi-plus-box-outline" size="30px"></v-icon>
      </v-btn>
      <span class="text">{{ count }}</span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const count = ref(0);

const props = defineProps({
  label: { type: String, required: true },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Fuzzy+Bubbles:wght@400;700&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

.counter-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: fixed;
}

.label-text {
  font-family: "Roboto", sans-serif;
  font-size: 1.4rem;
  color: #1d2d44;
  text-align: center;
  margin-bottom: 0.2rem;
}

.counter {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  width: 90px;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.text {
  font-family: "Roboto", sans-serif;
  font-size: 1.6rem;
  text-align: center;
  color: #1d2d44;
  padding: 0.5rem 0.7rem;
}
</style>
