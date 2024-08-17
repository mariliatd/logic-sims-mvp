<template>
  <span class="operators-color">
    <slot name="leftExpression"></slot> {{ operator }}
    <slot name="rightExpression"></slot>
  </span>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    operator: { type: String },
  },
});
</script>

<style></style>
