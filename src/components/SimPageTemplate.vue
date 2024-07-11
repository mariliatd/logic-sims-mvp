<template>
  <div class="template-box">
    <v-app>
      <v-row>
        <v-col cols="8">
          <div class="sim-box">
            <div class="sim-workspace">
              <slot name="workspace"></slot>
            </div>
            <v-icon icon="mdi-restore" size="60px" class="restore-sim"></v-icon>
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
  display: flex;
  flex-direction: column;
  margin: 1.2rem;
}

.restore-sim {
  bottom: -6rem;
  align-self: flex-end;
}

.code-box {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  margin: 1.2rem;
  height: 85%;
}

.sub-title {
  text-align: center;
  background-color: #eccbdf;
  border-radius: 1rem;
  padding: 0.5rem;
  margin: 1rem;
}
</style>
