<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate>
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-control">
          <ConditionalControl label="itemEscolhido" :content="items" />
        </div>
      </div>
    </template>
    <template #pseudocode>
      <div class="initial-code">
        <p class="pseudocode">// variável</p>
        <p class="pseudocode">
          total <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p id="running">leia (itemEscolhido)</p>
      </div>
    </template>
  </SimPageTemplate>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import ConditionalControl from "../components/ConditionalControl.vue";
import NavBar from "../components/NavBar.vue";
import SimPageTemplate from "../components/SimPageTemplate.vue";

export default defineComponent({
  components: {
    ConditionalControl,
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

.initial-code {
  margin: 1.2rem;
}

.pseudocode {
  padding-left: 1rem;
}

#running {
  background-color: #e9e8e8;
  border-radius: 1rem;
  padding: 0.2rem 1rem;
  margin-top: 0.5rem;
}
</style>
