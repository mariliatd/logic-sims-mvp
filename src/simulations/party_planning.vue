<template>
  <NavBar simName="Planejando a Festa" />
  <SimPageTemplate @sim="restoreSim()">
    <template #workspace>
      <div class="sim-workspace">
        <div class="conditional-loop-box">
          <ConditionalControl
            v-if="currentState > PartyPlanningSimState.VariableQuantidade"
            itemLabel="itemEscolhido"
            amountLabel="quantidade"
            :content="items"
            @selectedItem="selectItem"
            :selectedItem="selectedItem"
            :preparedItemList="preparedItemsList"
          />
          <div
            v-if="currentState >= PartyPlanningSimState.Loop2"
            class="loop-counter"
          >
            <LoopControl
              :selectedItem="selectedItem"
              :total="total"
              @totalPrepared="prepareItem"
              :totalPrepared="totalPrepared"
            />
          </div>
        </div>
        <div class="variable-display">
          <VariableDisplay name="itensProntos" :value="preparedItems" />
          <VariableDisplay
            v-if="currentState > PartyPlanningSimState.Loop1"
            name="quantidade"
            :value="total"
          />
          <VariableDisplay
            v-if="currentState > PartyPlanningSimState.VariableQuantidade"
            name="itemEscolhido"
            :value="selectedItemName"
          />
          <VariableDisplay
            v-if="selectedItem !== '' && !shouldShowConditionalDialog"
            name="totalPronto"
            :value="totalPrepared"
          />
        </div>
        <OutputDialog
          @closeOutputDialog="closeConditionalDialog"
          buttonText="Começar"
          :openOutputDialog="shouldShowConditionalDialog"
          :content="printConditionalMessage"
        />
        <OutputDialog
          @closeOutputDialog="closeLoopDialog"
          buttonText="Fechar"
          :openOutputDialog="shouldShowLoopDialog"
          :content="printLoopMessage"
        />
        <OutputDialog
          @closeOutputDialog="closeEndSimDialog"
          buttonText="Fechar"
          :openOutputDialog="shouldShowEndSimDialog"
          :content="printEndSimMessage"
        />
      </div>
    </template>
    <template #pseudocode>
      <div class="indent-code">
        <Variable
          name="itensProntos"
          value="0"
          :isAssignment="true"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.Initial)
              ? ['running', 'next-state']
              : '',
          ]"
          @click="
            currentState === PartyPlanningSimState.Initial
              ? (currentState = PartyPlanningSimState.Loop1)
              : null
          "
        />
        <Loop
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.Loop1)
              ? ['running', 'next-state']
              : '',
          ]"
          @click="
            currentState === PartyPlanningSimState.Loop1
              ? (currentState = PartyPlanningSimState.VariableQuantidade)
              : null
          "
        >
          <template #condition>
            <Operator operator="<">
              <template #leftExpression
                ><Variable name="itensProntos"
              /></template>
              <template #rightExpression>3</template>
            </Operator>
          </template>
        </Loop>
        <Variable
          name="quantidade"
          value="0"
          :isAssignment="true"
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.VariableQuantidade)
              ? ['running', 'next-state']
              : '',
          ]"
          @click="
            currentState === PartyPlanningSimState.VariableQuantidade
              ? (currentState = PartyPlanningSimState.ReadItem)
              : null
          "
        />
        <Input
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.ReadItem) ? 'running' : '',
          ]"
        >
          <template #content>
            <Variable name="itemEscolhido" />
          </template>
        </Input>
        <If
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.ConditionalCake) ? 'running' : '',
          ]"
        >
          <template #condition>
            <Operator operator="=">
              <template #leftExpression
                ><Variable name="itemEscolhido"
              /></template>
              <template #rightExpression>"bolo"</template>
            </Operator> </template
          >>
          <template #instructions>
            <Variable
              name="quantidade"
              value="1"
              :isAssignment="true"
              class="pl-7"
            />
            <Output class="pl-7">
              <template #content>"Prepare 1 bolo!"</template>
            </Output>
          </template>
        </If>
        <div class="pl-6">
          <Else
            :class="[
              'pseudocode',
              isRunning(PartyPlanningSimState.ConditionalBalloon)
                ? 'running'
                : '',
            ]"
          >
            <template #instructions>
              <If class="pl-7">
                <template #condition>
                  <Operator operator="=">
                    <template #leftExpression
                      ><Variable name="itemEscolhido"
                    /></template>
                    <template #rightExpression>"balão"</template>
                  </Operator>
                </template>
                <template #instructions>
                  <Variable
                    name="quantidade"
                    value="10"
                    :isAssignment="true"
                    class="pl-7"
                  />
                  <Output class="pl-7">
                    <template #content>"Prepare 10 balões!"</template>
                  </Output>
                </template>
              </If>
            </template>
          </Else>
          <Else
            class="pl-11"
            :class="[
              'pseudocode',
              isRunning(PartyPlanningSimState.ConditionalCandy)
                ? 'running'
                : '',
            ]"
          >
            <template #instructions>
              <Variable
                name="quantidade"
                value="20"
                :isAssignment="true"
                class="pl-7"
              />
              <Output class="pl-7">
                <template #content>"Prepare 20 doces!"</template>
              </Output>
            </template>
          </Else>
        </div>
        <Variable
          name="totalPronto"
          value="0"
          :isAssignment="true"
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.VariableTotalPronto)
              ? ['running', 'next-state']
              : '',
          ]"
          @click="
            currentState === PartyPlanningSimState.VariableTotalPronto
              ? (currentState = PartyPlanningSimState.Loop2)
              : null
          "
        />
        <Loop
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.Loop2) ? 'running' : '',
          ]"
        >
          <template #condition>
            <Operator operator="<">
              <template #leftExpression
                ><Variable name="totalPronto"
              /></template>
              <template #rightExpression
                ><Variable name="quantidade"
              /></template>
            </Operator>
          </template>
          <template #instructions>
            <p class="pl-7">prepare 1 <Variable name="{itemEscolhido}" /></p>
            <Variable
              name="totalPronto"
              value="totalPronto + 1"
              :isAssignment="true"
              class="pl-7"
            />
          </template>
        </Loop>
        <Variable
          name="itensProntos"
          value="itensProntos + 1"
          :isAssignment="true"
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.IncrementItensProntos)
              ? ['running', 'next-state']
              : '',
          ]"
          @click="
            currentState === PartyPlanningSimState.IncrementItensProntos
              ? openLoopDialog()
              : null
          "
        />
        <Output
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.WriteItemPronto) ? 'running' : '',
          ]"
        >
          <template #content>"O item {itemEscolhido} está pronto!"</template>
        </Output>
        <Output
          :class="[
            'pseudocode',
            isRunning(PartyPlanningSimState.Final) ? 'running' : '',
          ]"
        >
          <template #content>"A festa está pronta!!!"</template>
        </Output>
      </div>
    </template>
  </SimPageTemplate>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { PartyPlanningSimState } from "@/enums";

import ConditionalControl from "@/components/simulation/ConditionalControl.vue";
import NavBar from "@/components/NavBar.vue";
import SimPageTemplate from "@/components/SimPageTemplate.vue";
import LoopControl from "@/components/simulation/LoopControl.vue";
import VariableDisplay from "@/components/simulation/VariableDisplay.vue";
import OutputDialog from "@/components/simulation/OutputDialog.vue";
import Variable from "@/components/pseudocode/Variable.vue";
import Operator from "@/components/pseudocode/Operator.vue";
import Loop from "@/components/pseudocode/Loop.vue";
import Input from "@/components/pseudocode/Input.vue";
import Output from "@/components/pseudocode/Output.vue";
import If from "@/components/pseudocode/If.vue";
import Else from "@/components/pseudocode/Else.vue";

export default defineComponent({
  components: {
    ConditionalControl,
    LoopControl,
    NavBar,
    OutputDialog,
    SimPageTemplate,
    VariableDisplay,
    Variable,
    Operator,
    Loop,
    Input,
    Output,
    If,
    Else,
  },
  data: () => ({
    PartyPlanningSimState: PartyPlanningSimState,
    currentState: PartyPlanningSimState.Initial,
    items: [
      {
        name: "birthday_cake",
        text: "bolo de aniversário",
        path: "/assets/birthday-cake.svg",
        label: "1",
        size: 4,
      },
      {
        name: "balloon",
        text: "balão",
        path: "/assets/balloon.svg",
        label: "10",
        size: 4,
      },
      {
        name: "party_candy",
        text: "doce de festa",
        path: "/assets/party-candy.svg",
        label: "20",
        size: 4,
      },
    ],
    selectedItem: "",
    selectedItemName: "",
    total: 0,
    totalPrepared: 0,
    printConditionalMessage: "",
    printLoopMessage: "",
    printEndSimMessage: "",
    shouldShowConditionalDialog: false,
    shouldShowLoopDialog: false,
    shouldShowEndSimDialog: false,
    preparedItems: 0,
    preparedItemsList: [] as String[],
  }),
  methods: {
    selectItem(value: string) {
      console.log("selected item", value);
      this.selectedItem = value;

      if (this.selectedItem == "birthday_cake") {
        this.total = 1;
        this.selectedItemName = "bolo";
        this.currentState = PartyPlanningSimState.ConditionalCake;
        this.printConditionalMessage = "Prepare 1 bolo!";
      } else if (this.selectedItem == "balloon") {
        this.total = 10;
        this.selectedItemName = "balão";
        this.currentState = PartyPlanningSimState.ConditionalBalloon;
        this.printConditionalMessage = "Prepare 10 balões!";
      } else if (this.selectedItem == "party_candy") {
        this.total = 20;
        this.selectedItemName = "doce";
        this.currentState = PartyPlanningSimState.ConditionalCandy;
        this.printConditionalMessage = "Prepare 20 doces!";
      } else {
        console.error("No item selected");
      }

      this.shouldShowConditionalDialog = true;
    },
    closeConditionalDialog(value: boolean) {
      this.shouldShowConditionalDialog = value;
      this.currentState = PartyPlanningSimState.VariableTotalPronto;
    },
    openLoopDialog() {
      this.currentState = PartyPlanningSimState.WriteItemPronto;
      this.shouldShowLoopDialog = true;
    },
    closeLoopDialog(value: boolean) {
      this.shouldShowLoopDialog = value;

      if (this.preparedItems === 3) {
        this.printEndSimMessage = "A festa está pronta!!!";
        setTimeout(
          () => (this.currentState = PartyPlanningSimState.Final),
          500
        );
        setTimeout(() => (this.shouldShowEndSimDialog = true), 500);
      } else {
        this.restartLoop();
      }
    },
    closeEndSimDialog(value: boolean) {
      this.shouldShowEndSimDialog = value;
      this.restoreSim();
    },
    prepareItem(value: number) {
      console.log("total prepared", value);
      this.totalPrepared = value;

      if (this.preparedItemsList.includes(this.selectedItem)) {
        return;
      }

      if (this.totalPrepared === this.total) {
        this.currentState = PartyPlanningSimState.IncrementItensProntos;
        this.preparedItems++;
        this.preparedItemsList.push(this.selectedItem);
        this.printLoopMessage = `O item ${this.selectedItemName} está pronto!`;
      }
    },
    isRunning(codeState: PartyPlanningSimState) {
      return codeState === this.currentState;
    },
    restartLoop() {
      this.currentState = PartyPlanningSimState.Loop1;
      this.selectedItem = "";
      this.selectedItemName = "";
      this.total = 0;
      this.totalPrepared = 0;
    },
    restoreSim() {
      this.currentState = PartyPlanningSimState.Initial;
      this.selectedItem = "";
      this.selectedItemName = "";
      this.total = 0;
      this.totalPrepared = 0;
      this.preparedItems = 0;
      this.preparedItemsList = [];
    },
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
  gap: 1rem;
  margin-top: 2rem;
  margin-left: 2rem;
}

.indent-code {
  margin: 0.5rem;
}

.pseudocode {
  padding: 0.1rem 1rem;
}

.next-state {
  cursor: pointer;
}

.running {
  background-color: #e9e8e8;
  border-radius: 1rem;
}
</style>
