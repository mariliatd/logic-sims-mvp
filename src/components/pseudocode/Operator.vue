<template>
  <span class="operators-color">
    <slot name="leftExpression"></slot> {{ operator }}
    <slot name="rightExpression"></slot>
    <v-tooltip activator="parent" location="bottom">operadores</v-tooltip>
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

<style>
.operators-color {
  display: inline;
  /* background-color: #d0f4de;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.operators-color:hover {
  background-color: #d0f4de;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
