<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate @sim="restoreSim()">
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-control">
          <ConditionalControl
            label="itemEscolhido"
            :content="items"
            @item="selectItem"
          />
        </div>
        <div v-if="selectedItem == 'birthday_cake'" class="loop-counter-object">
          <div>
            <img src="../assets/bake.svg" alt="fogão" width="200px" height="200px">
          </div>
        </div>
        <div v-if="selectedItem == 'balloon'" class="loop-counter-object">
          <div>
            <img src="../assets/gas-cylinder.svg" alt="cilindro de gás" width="200px" height="200px">
          </div>
        </div>
        <div v-if="selectedItem == 'party_candy'" class="loop-counter-object">
          <div>
            <img src="../assets/plate.svg" alt="prato" width="250px" height="200px">
            <img src="../assets/plate.svg" alt="prato" width="250px" height="200px" style="position: relative; bottom: 5rem;">
          </div>
        </div>
        <div v-if="selectedItem != ''" class="loop-counter">
          <LoopCounter label="totalPronto" />
        </div>
      </div>
    </template>
    <template #pseudocode>
      <div class="initial-code">
        <p class="pseudocode">// variável</p>
        <p class="pseudocode">
          total <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p :class="['pseudocode', isRunning('initial') ? 'running' : '']"><b>leia</b> (itemEscolhido)</p>
        <p :class="['pseudocode', isRunning('conditional_cake') ? 'running' : '']" v-if="selectedItem != ''">
          <b>se</b> itemEscolhido = "bolo" <b>então</b> <br />
          <p class="pl-7">total <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 1</p>
        </p>
        <p :class="['pseudocode', isRunning('conditional_balloon') ? 'running' : '']" v-if="selectedItem != ''">
          <b>senão</b> <br />
          <p class="pl-7"><b>se</b> itemEscolhido = "balão" <b>então</b> <br /></p>
          <p class="pl-14">total <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10</p>
        </p>
        <p :class="['pseudocode', isRunning('conditional_candy') ? 'running' : '']" v-if="selectedItem != ''">
          <p class="pl-7"><b>senão</b> <br /></p>
          <p class="pl-14">total <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 20</p>
        </p>
      </div>
    </template>
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
    currentState: "initial",
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
    selectedItem: "",
    total: 0,
  }),
  methods: {
    selectItem(value: string) {
      console.log(value);
      this.selectedItem = value;

      if (this.selectedItem == "birthday_cake") {
        this.total = 1;
        this.currentState = "conditional_cake";
      } else if (this.selectedItem == "balloon") {
        this.total = 10;
        this.currentState = "conditional_balloon";
      } else if (this.selectedItem == "party_candy") {
        this.total = 20;
        this.currentState = "conditional_candy";
      } else {
        console.error("No item selected");
      }
    },
    isRunning(codeState: string) {
      return codeState == this.currentState;
    },
    restoreSim() {
      this.currentState = "initial";
      this.selectedItem = "";
      this.total = 0;
    }
  },
});
</script>

<style>
.sim-workspace {
  display: flex;
  flex-direction: column;
}

.loop-counter-object {
  margin: 15rem 8rem;
}

.loop-counter {
  align-self: flex-end;
  margin-top: -27rem;
}

.initial-code {
  margin: 1.2rem;
}

.pseudocode {
  padding: 0.2rem 1rem;
}

.running {
  background-color: #e9e8e8;
  border-radius: 1rem;
}
</style>
