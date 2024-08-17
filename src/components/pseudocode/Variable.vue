<template>
  <p v-if="isAssignment" class="variable-color">
    {{ name }}
    <v-icon icon="mdi-arrow-left" size="20px"></v-icon>
    {{ value }}
  </p>
  <span v-else class="variable-color">{{ name }}</span>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    name: { type: String, required: true },
    value: { type: String },
    isAssignment: { type: Boolean, default: false },
  },
});
</script>

<style></style>
