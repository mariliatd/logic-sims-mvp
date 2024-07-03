<template>
  <div class="template-box">
    <v-app>
      <v-row>
        <v-col cols="8">
          <div class="sim-box">
            <slot name="workspace"></slot>
          </div>
        </v-col>
        <v-col cols="4">
          <div class="code-box">
            <p class="sub-title">Pseudocódigo</p>
            <slot name="pseudocode"></slot>
          </div>
        </v-col>
      </v-row>
    </v-app>
  </div>
</template>

<script setup lang="ts"></script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Fuzzy+Bubbles:wght@400;700&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

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

.sim-box {
  margin: 1.2rem;
}

.code-box {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  margin: 1.2rem;
}

.sub-title {
  font-family: "Roboto", sans-serif;
  font-size: 1.4rem;
  text-align: center;
  color: #1d2d44;
  background-color: #eccbdf;
  border-radius: 1rem;
  padding: 0.5rem;
  margin: 1rem;
}
</style>
