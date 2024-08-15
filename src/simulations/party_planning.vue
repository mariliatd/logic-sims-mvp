<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate @sim="restoreSim()">
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-loop-box">
          <ConditionalControl
            itemLabel="itemEscolhido"
            amountLabel="quantidade"
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
          <VariableDisplay v-if="selectedItem !== '' && !shouldShowDialog" label="totalPronto" :value="totalPrepared" />
        </div>
        <OutputDialog @closeOutputDialog="closeDialog" :openOutputDialog="shouldShowDialog" :content="printMessage"/>
      </div>
    </template>
    <template #pseudocode>
      <div class="indent-code">
        <p :class="['pseudocode', isRunning('variable_quantidade') ? 'running' : '']">
          quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p :class="['pseudocode', isRunning('read_item') ? 'running' : '']"><b>leia</b> (itemEscolhido)</p>
        <p :class="['pseudocode', isRunning('conditional_cake') ? 'running' : '']">
          <b>se</b> itemEscolhido = "bolo" <b>então</b> <br />
          <p class="pl-7">quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 1</p>
          <p class="pl-7"><b>escreva</b> ("Prepare 1 bolo!")</p>
        </p>
        <p :class="['pseudocode', isRunning('conditional_balloon') ? 'running' : '']">
          <b>senão</b> <br />
          <p class="pl-7"><b>se</b> itemEscolhido = "balão" <b>então</b> <br /></p>
          <p class="pl-14">quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10</p>
          <p class="pl-14"><b>escreva</b> ("Prepare 10 balões!")</p>
        </p>
        <p :class="['pseudocode', isRunning('conditional_candy') ? 'running' : '']">
          <p class="pl-7"><b>senão</b> <br /></p>
          <p class="pl-14">quantidade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 20</p>
          <p class="pl-14"><b>escreva</b> ("Prepare 20 doces!")</p>
        </p>
        <p :class="['pseudocode', isRunning('variable_totalPronto') ? 'running' : '']">
          totalPronto <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p :class="['pseudocode', isRunning('loop') ? 'running' : '']">
          <b>enquanto</b> totalPronto < quantidade <b>faça</b>
          <p class="pl-7">prepare 1 itemEscolhido</p>
          <p class="pl-7"> totalPronto <v-icon icon="mdi-arrow-left" size="20px"></v-icon> totalPronto + 1</p>
        </p>
        <p></p>
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
import OutputDialog from "@/components/OutputDialog.vue";

export default defineComponent({
  components: {
    ConditionalControl,
    LoopCounter,
    NavBar,
    OutputDialog,
    SimPageTemplate,
    VariableDisplay,
  },
  data: () => ({
    currentState: "",
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
    printMessage: "",
    shouldShowDialog: false,
  }),
  methods: {
    selectItem(value: string) {
      console.log('selected item', value);
      this.selectedItem = value;

      if (this.selectedItem == "birthday_cake") {
        this.total = 1;
        this.selectedItemName = "bolo"
        this.currentState = "conditional_cake";
        this.printMessage = "Prepare 1 bolo!";
      } else if (this.selectedItem == "balloon") {
        this.total = 10;
        this.selectedItemName = "balão"
        this.currentState = "conditional_balloon";
        this.printMessage = "Prepare 10 balões!";
      } else if (this.selectedItem == "party_candy") {
        this.total = 20;
        this.selectedItemName = "doce"
        this.currentState = "conditional_candy";
        this.printMessage = "Prepare 20 doces!";
      } else {
        console.error("No item selected");
      }

      this.shouldShowDialog = true;
    },
    closeDialog(value: boolean) {
      this.shouldShowDialog = value;
      this.currentState = "variable_totalPronto";
      setTimeout(() => this.currentState = "loop", 500);
    },
    prepareItem(value: number) {
      console.log('total prepared', value);
      this.totalPrepared = value;
    },
    isRunning(codeState: string) {
      return codeState == this.currentState;
    },
    restoreSim() {
      this.currentState = "variable_quantidade";
      setTimeout(() => this.currentState = "read_item", 500);
      this.selectedItem = "";
      this.selectedItemName = ""
      this.total = 0;
      this.totalPrepared = 0;
    }
  },
  mounted() {
    this.currentState = "variable_quantidade";
    setTimeout(() => this.currentState = "read_item", 500);
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
  margin: 1rem;
}

.pseudocode {
  padding: 0.2rem 1rem;
}

.running {
  background-color: #e9e8e8;
  border-radius: 1rem;
}
</style>
