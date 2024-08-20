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
            :preparedItemList="preparedItemsList"
          />
          <div v-if="selectedItem !== ''" class="loop-counter">
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
          <VariableDisplay name="itemEscolhido" :value="selectedItemName" />
          <VariableDisplay name="quantidade" :value="total" />
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
            isRunning('variable_itensProntos') ? 'running' : '',
          ]"
        />
        <Loop :class="['pseudocode', isRunning('loop_1') ? 'running' : '']">
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
            isRunning('variable_quantidade') ? 'running' : '',
          ]"
        />
        <Input
          class="pl-10"
          :class="['pseudocode', isRunning('read_item') ? 'running' : '']"
        >
          <template #content>
            <Variable name="itemEscolhido" />
          </template>
        </Input>
        <If
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning('conditional_cake') ? 'running' : '',
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
              isRunning('conditional_balloon') ? 'running' : '',
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
              isRunning('conditional_candy') ? 'running' : '',
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
            isRunning('variable_totalPronto') ? 'running' : '',
          ]"
        />
        <Loop
          class="pl-10"
          :class="['pseudocode', isRunning('loop_2') ? 'running' : '']"
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
            <p class="pl-7">prepare 1 <Variable name="itemEscolhido" /></p>
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
            isRunning('increment_itensProntos') ? 'running' : '',
          ]"
        />
        <Output
          class="pl-10"
          :class="[
            'pseudocode',
            isRunning('write_itemPronto') ? 'running' : '',
          ]"
        >
          <template #content>"O itemEscolhido está pronto!"</template>
        </Output>
        <Output :class="['pseudocode', isRunning('end_sim') ? 'running' : '']">
          <template #content>"A festa está pronta!!!"</template>
        </Output>
      </div>
    </template>
  </SimPageTemplate>
</template>

<script lang="ts">
import { defineComponent } from "vue";

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
        this.currentState = "conditional_cake";
        this.printConditionalMessage = "Prepare 1 bolo!";
      } else if (this.selectedItem == "balloon") {
        this.total = 10;
        this.selectedItemName = "balão";
        this.currentState = "conditional_balloon";
        this.printConditionalMessage = "Prepare 10 balões!";
      } else if (this.selectedItem == "party_candy") {
        this.total = 20;
        this.selectedItemName = "doce";
        this.currentState = "conditional_candy";
        this.printConditionalMessage = "Prepare 20 doces!";
      } else {
        console.error("No item selected");
      }

      this.shouldShowConditionalDialog = true;
    },
    closeConditionalDialog(value: boolean) {
      this.shouldShowConditionalDialog = value;
      this.currentState = "variable_totalPronto";
      setTimeout(() => (this.currentState = "loop_2"), 500);
    },
    closeLoopDialog(value: boolean) {
      this.shouldShowLoopDialog = value;

      if (this.preparedItems === 3) {
        this.printEndSimMessage = "A festa está pronta!!!";
        setTimeout(() => (this.currentState = "end_sim"), 500);
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

      if (this.totalPrepared === this.total) {
        this.currentState = "increment_itensProntos";
        this.preparedItems++;
        this.preparedItemsList.push(this.selectedItem);
        this.printLoopMessage = "O itemEscolhido está pronto!";

        setTimeout(() => (this.currentState = "write_itemPronto"), 500);
        setTimeout(() => (this.shouldShowLoopDialog = true), 500);
      }
    },
    isRunning(codeState: string) {
      return codeState == this.currentState;
    },
    restartLoop() {
      this.currentState = "loop_1";
      setTimeout(() => (this.currentState = "variable_quantidade"), 500);
      setTimeout(() => (this.currentState = "read_item"), 1000);

      this.selectedItem = "";
      this.selectedItemName = "";
      this.total = 0;
      this.totalPrepared = 0;
    },
    restoreSim() {
      this.currentState = "variable_itensProntos";
      setTimeout(() => (this.currentState = "loop_1"), 500);
      setTimeout(() => (this.currentState = "variable_quantidade"), 1000);
      setTimeout(() => (this.currentState = "read_item"), 1500);

      this.selectedItem = "";
      this.selectedItemName = "";
      this.total = 0;
      this.totalPrepared = 0;
      this.preparedItems = 0;
      this.preparedItemsList = [];
    },
  },
  mounted() {
    this.currentState = "variable_itensProntos";
    setTimeout(() => (this.currentState = "loop_1"), 500);
    setTimeout(() => (this.currentState = "variable_quantidade"), 1000);
    setTimeout(() => (this.currentState = "read_item"), 1500);
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

.running {
  background-color: #e9e8e8;
  border-radius: 1rem;
}
</style>
