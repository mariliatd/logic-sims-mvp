<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate @sim="restoreSim()">
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-loop-box">
          <ConditionalControl
            label="itemEscolhido"
            :content="items"
            @selectedItem="selectItem"
            :selectedItem="selectedItem"
          />
          <div v-if="selectedItem !== ''" class="loop-counter">
            <LoopCounter :selectedItem="selectedItem" :total="total" @totalPrepared="prepareItem" :totalPrepared="totalPrepared"/>
          </div>
        </div>
        <div class="variable-display">
          <VariableDisplay label="quantidade" :value="total" />
          <VariableDisplay label="itemEscolhido" :value="selectedItemName" />
          <VariableDisplay v-if="selectedItem !== ''" label="totalPronto" :value="totalPrepared" />
        </div>
      </div>
    </template>
    <template #pseudocode>
      <div class="indent-code">
        <p class="pseudocode">
          quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p :class="['pseudocode', isRunning('initial') ? 'running' : '']"><b>leia</b> (itemEscolhido)</p>
        <p :class="['pseudocode', isRunning('conditional_cake') ? 'running' : '']">
          <b>se</b> itemEscolhido = "bolo" <b>então</b> <br />
          <p class="pl-7">quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 1</p>
        </p>
        <p :class="['pseudocode', isRunning('conditional_balloon') ? 'running' : '']">
          <b>senão</b> <br />
          <p class="pl-7"><b>se</b> itemEscolhido = "balão" <b>então</b> <br /></p>
          <p class="pl-14">quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10</p>
        </p>
        <p :class="['pseudocode', isRunning('conditional_candy') ? 'running' : '']">
          <p class="pl-7"><b>senão</b> <br /></p>
          <p class="pl-14">quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 20</p>
        </p>
        <p class="pseudocode">
          totalPronto <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p class="pseudocode">
          <b>enquanto</b> totalPronto < quantidade <b>faça</b>
          <p class="pl-7"> totalPronto <v-icon icon="mdi-arrow-left" size="20px"></v-icon> totalPronto + 1</p>
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
import VariableDisplay from "@/components/VariableDisplay.vue";

export default defineComponent({
  components: {
    ConditionalControl,
    LoopCounter,
    NavBar,
    SimPageTemplate,
    VariableDisplay,
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
    selectedItemName: "",
    total: 0,
    totalPrepared: 0,
  }),
  methods: {
    selectItem(value: string) {
      console.log('selected item', value);
      this.selectedItem = value;

      if (this.selectedItem == "birthday_cake") {
        this.total = 1;
        this.selectedItemName = "bolo"
        this.currentState = "conditional_cake";
      } else if (this.selectedItem == "balloon") {
        this.total = 10;
        this.selectedItemName = "balão"
        this.currentState = "conditional_balloon";
      } else if (this.selectedItem == "party_candy") {
        this.total = 20;
        this.selectedItemName = "doce"
        this.currentState = "conditional_candy";
      } else {
        console.error("No item selected");
      }
    },
    prepareItem(value: number) {
      console.log('total prepared', value);
      this.totalPrepared = value;
    },
    isRunning(codeState: string) {
      return codeState == this.currentState;
    },
    restoreSim() {
      this.currentState = "initial";
      this.selectedItem = "";
      this.selectedItemName = ""
      this.total = 0;
      this.totalPrepared = 0;
    }
  },
});
</script>

<style>
.sim-workspace {
  display: flex;
  width: 100%;
  height: 100%;
}

.conditional-loop-box {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.loop-counter {
  margin: 15rem 5rem;
}

.variable-display {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-top: 2rem;
  margin-left: 2rem;
}

.indent-code {
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
