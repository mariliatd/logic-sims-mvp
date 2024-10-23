<template>
  <p>
    <span class="if-color">
      <b>se</b> <slot name="condition"></slot> <b>então</b>
      <v-tooltip activator="parent">condicional (se)</v-tooltip>
    </span>
    <slot name="instructions"></slot>
  </p>
</template>

<style>
.if-color {
  display: inline;
  /* background-color: #e4c1f9;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.if-color:hover {
  background-color: #e4c1f9;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
