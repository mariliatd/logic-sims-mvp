<template>
  <div class="template-box">
    <v-app>
      <v-row>
        <v-col cols="8"><SimWorkspace /></v-col>
        <v-col cols="4"><Pseudocode /></v-col>
      </v-row>
    </v-app>
  </div>
</template>

<script setup lang="ts">
import Pseudocode from "./Pseudocode.vue";
import SimWorkspace from "./SimWorkspace.vue";
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  height: 100%;
  overflow: hidden;
}

.template-box {
  position: absolute;
  top: 4.7rem;
  bottom: 1.2rem;
  left: 1.2rem;
  right: 1.2rem;
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  overflow: hidden;
}
</style>
