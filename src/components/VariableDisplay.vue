<template>
  <div class="variable-box">
    <p class="label-text">{{ label }}</p>
    <div class="variable">
      <span class="text">{{ value }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    label: { type: String, required: true },
    value: { type: Number, required: true },
  },
});
</script>

<style>
.variable-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.label-text {
  text-align: center;
  margin-bottom: 0.2rem;
}

.variable {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  background-color: #e9e8e8;
  width: 80px;
  height: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.text {
  font-size: 1.8rem;
}
</style>
