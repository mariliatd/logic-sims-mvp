<template>
  <PartyPlanning />
</template>

<script setup lang="ts">
import PartyPlanning from "./simulations/party_planning.vue";
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");

body {
  font-family: "Roboto", sans-serif;
  font-size: 1.3rem;
  color: #1d2d44;
}

@media screen and (min-width: 360px) and (max-width: 1080px) {
  body {
    font-size: 0.9rem;
  }
}
</style>
