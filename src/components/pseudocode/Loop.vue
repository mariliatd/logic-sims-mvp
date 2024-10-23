<template>
  <p>
    <span class="loop-color">
      <b>enquanto</b> <slot name="condition"></slot> <b>faça</b>
      <v-tooltip activator="parent" location="top">laço de repetição</v-tooltip>
    </span>
    <slot name="instructions"></slot>
  </p>
</template>

<style>
.loop-color {
  display: inline;
  /* background-color: #a9def9;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.loop-color:hover {
  background-color: #a9def9;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
