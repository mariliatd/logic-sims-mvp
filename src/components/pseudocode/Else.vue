<template>
  <p>
    <span class="else-color">
      <b>senão</b>
      <v-tooltip activator="parent">condicional (senão)</v-tooltip>
    </span>
    <slot name="instructions"></slot>
  </p>
</template>

<style>
.else-color {
  display: inline;
  /* background-color: #e4c1f9;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.else-color:hover {
  background-color: #e4c1f9;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
