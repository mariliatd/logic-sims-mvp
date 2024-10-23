<template>
  <p v-if="isAssignment">
    <span class="variable-color">
      {{ name }}
      <v-icon icon="mdi-arrow-left" size="20px"></v-icon>
      {{ value }}
    </span>
    <v-tooltip activator="parent">variável</v-tooltip>
  </p>
  <p v-else-if="valueHasOperation">
    <span class="variable-color">
      {{ name }}
      <v-icon icon="mdi-arrow-left" size="20px"></v-icon>
      <slot name="operation"></slot>
    </span>
    <v-tooltip activator="parent">variável</v-tooltip>
  </p>
  <span v-else class="variable-color">
    {{ name }}
    <v-tooltip activator="parent">variável</v-tooltip>
  </span>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    name: { type: String, required: true },
    value: { type: String },
    isAssignment: { type: Boolean, default: false },
    valueHasOperation: { type: Boolean, default: false },
  },
});
</script>

<style>
.variable-color {
  display: inline;
  /* background-color: #f9f1a8;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.variable-color:hover {
  background-color: #f9f1a8;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
