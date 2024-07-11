<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate>
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-control">
          <ConditionalControl label="itemEscolhido" :content="items" />
        </div>
        <div class="loop-counter">
          <LoopCounter label="totalPronto" />
        </div>
      </div>
    </template>
    <template #pseudocode> </template>
  </SimPageTemplate>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import ConditionalControl from "../components/ConditionalControl.vue";
import NavBar from "../components/NavBar.vue";
import SimPageTemplate from "../components/SimPageTemplate.vue";
import LoopCounter from "@/components/LoopCounter.vue";

export default defineComponent({
  components: {
    ConditionalControl,
    LoopCounter,
    NavBar,
    SimPageTemplate,
  },
  data: () => ({
    items: [
      {
        name: "birthday_cake",
        text: "bolo de aniversário",
        path: "src/assets/birthday-cake.svg",
        label: "1",
        size: 4,
      },
      {
        name: "balloon",
        text: "balão",
        path: "src/assets/balloon.svg",
        label: "10",
        size: 4,
      },
      {
        name: "party_candy",
        text: "doce de festa",
        path: "src/assets/party-candy.svg",
        label: "20",
        size: 4,
      },
    ],
  }),
});
</script>

<style>
.sim-workspace {
  display: flex;
  flex-direction: column;
}

.loop-counter {
  align-self: flex-end;
  margin-top: 15rem;
}
</style>
