<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate @sim="restoreSim()">
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-control">
          <ConditionalControl
            label="itemEscolhido"
            :content="items"
            @selectedItem="selectItem"
            :selectedItem="selectedItem"
          />
        </div>
        <div v-if="selectedItem == 'birthday_cake'" class="loop-counter-object">
          <div>
            <img src="../assets/bake.svg" alt="fogão" width="200px" height="200px">
          </div>
          <div v-for="index in totalToPrepare" :key="index" id="cake-prepared">
            <img src="../assets/birthday-cake.svg" alt="bolo de aniversário" width="100px" height="100px">
          </div>
        </div>
        <div v-if="selectedItem == 'balloon'" class="loop-counter-object">
          <div>
            <img src="../assets/gas-cylinder.svg" alt="cilindro de gás" width="200px" height="200px">
          </div>
          <div id="balloon-box">
            <div v-for="index in totalToPrepare" :key="index" id="balloon-prepared">
              <img src="../assets/balloon.svg" alt="balão" width="100px" height="100px">
            </div>
          </div>
        </div>
        <div v-if="selectedItem == 'party_candy'" class="loop-counter-object" id="plate-candy-box">
          <div>
            <img src="../assets/plate.svg" alt="prato" width="250px" height="200px">
            <img src="../assets/plate.svg" alt="prato" width="250px" height="200px" style="margin-left: -3rem;">
          </div>
          <div id="candy-box">
            <div v-for="index in totalToPrepare" :key="index" id="candy-prepared">
              <img src="../assets/party-candy.svg" alt="doce de festa" width="50px" height="50px">
            </div>
          </div>
        </div>
        <div v-if="selectedItem != ''" class="loop-counter">
          <LoopCounter label="totalPronto" @totalPrepared="prepareItem" :total="total"/>
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
    totalToPrepare: 0,
  }),
  methods: {
    selectItem(value: string) {
      console.log('selected item', value);
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
    prepareItem(value: number) {
      console.log('total to prepare', value);
      this.totalToPrepare = value;
    },
    isRunning(codeState: string) {
      return codeState == this.currentState;
    },
    restoreSim() {
      this.currentState = "initial";
      this.selectedItem = "";
      this.total = 0;
      this.totalToPrepare = 0;
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
  display: flex;
}

#party-candy {
  align-self: center;
}

#cake-prepared {
  margin-left: 10rem;
}

#balloon-box {
  display: flex;
  flex-wrap: wrap;
  width: 50%;
  justify-content: center;
}

#balloon-prepared {
  margin-top: -10rem;
  margin-left: -2rem;
}

#plate-candy-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#candy-box {
  display: flex;
  width: 50%;
  margin-left: 8rem;
}

#candy-prepared {
  margin-top: -11.3rem;
  margin-left: -2rem;
}

.loop-counter {
  align-self: flex-end;
  margin-top: -27rem;
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
