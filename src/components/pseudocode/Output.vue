<template>
  <p>
    <span class="output-color">
      <b>escreva</b> (<slot name="content"></slot>)
      <v-tooltip activator="parent" location="start">saída</v-tooltip>
    </span>
  </p>
</template>

<style>
.output-color {
  display: inline;
  /* background-color: #ffc17c;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.output-color:hover {
  background-color: #ffc17c;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
