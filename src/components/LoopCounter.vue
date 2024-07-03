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
.counter-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: fixed;
}

.label-text {
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
  font-size: 1.6rem;
  text-align: center;
  padding: 0.5rem 0.7rem;
}
</style>
