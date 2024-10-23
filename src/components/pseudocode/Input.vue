<template>
  <p>
    <span class="input-color">
      <b>leia</b> (<slot name="content"></slot>)
      <v-tooltip activator="parent" location="start">entrada</v-tooltip>
    </span>
  </p>
</template>

<style>
.input-color {
  display: inline;
  /* background-color: #ffc17c;
  border-radius: 1rem;
  padding: 0 0.5rem; */
}

.input-color:hover {
  background-color: #ffc17c;
  border-radius: 1rem;
  padding: 0 0.5rem;
}
</style>
