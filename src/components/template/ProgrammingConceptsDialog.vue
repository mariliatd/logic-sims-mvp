<template>
  <v-dialog v-model="openDialog" @click:outside="close" width="1500px">
    <v-card height="800px">
      <p class="dialog-fuzzy dialog-title">Conceitos de Programação</p>
      <v-row class="ml-3">
        <v-col cols="3">
          <div
            class="dialog-fuzzy dialog-sub-title side-menu mb-3"
            @click="concept = 'pseudocode'"
          >
            O que é um pseudocódigo?
          </div>
          <div
            class="dialog-fuzzy dialog-sub-title side-menu mb-3"
            @click="concept = 'variable'"
          >
            Variáveis
          </div>
          <div
            class="dialog-fuzzy dialog-sub-title side-menu mb-3"
            @click="concept = 'inputOutput'"
          >
            Entrada e Saída
          </div>
          <div
            class="dialog-fuzzy dialog-sub-title side-menu mb-3"
            @click="concept = 'operators'"
          >
            Operadores
          </div>
          <div
            class="dialog-fuzzy dialog-sub-title side-menu mb-3"
            @click="concept = 'conditional'"
          >
            Condicional
          </div>
          <div
            class="dialog-fuzzy dialog-sub-title side-menu mb-3"
            @click="concept = 'loop'"
          >
            Laço de repetição
          </div>
        </v-col>
        <v-col cols="9">
          <div v-if="concept == 'pseudocode'" class="definition">
            <p class="dialog-fuzzy dialog-sub-title mb-4">
              O que é um pseudocódigo?
            </p>
            <p>
              É uma forma de escrever um
              <span class="dialog-fuzzy">algoritmo</span> com uma linguagem
              simples, sem necessidade de conhecer uma linguagem de programação
              específica.
            </p>
            <p>
              Um <span class="dialog-fuzzy">algoritmo</span> é qualquer
              sequência finita de passos para resolver um problema ou completar
              tarefa. É como dizemos para um computador o que queremos que ele
              faça.
            </p>
            <img
              src="@/assets/concepts_pseudocode.png"
              alt="exemplo de pseudocódigo"
              class="mt-3"
              style="height: 90%; width: 90%; margin-left: 2rem"
            />
          </div>
          <div v-if="concept == 'variable'" class="definition">
            <p class="dialog-fuzzy dialog-sub-title mb-4">Variáveis</p>
            <p>
              São espaços na memória do computador que guardam algum dado ou
              informação. Esses valores armazenados podem ou não ser alterados
              ao longo do programa.
            </p>
            <img
              src="@/assets/concepts_variables.png"
              alt="exemplo de variáveis"
              class="mt-3"
              style="height: 90%; width: 90%; margin-left: 2rem"
            />
          </div>
          <div v-if="concept == 'inputOutput'" class="definition">
            <p class="dialog-fuzzy dialog-sub-title mb-4">Entrada e Saída</p>
            <p>
              A entrada de um algoritmo é algum dado recebido pelo computador,
              que será processado para produzir um resultado, que será a saída
              do programa.
            </p>
            <img
              src="@/assets/concepts_input_output_cake.png"
              alt="exemplo de entrada e saída"
              class="my-3"
              style="height: 50%; width: 50%; margin-left: 10rem"
            />
            <p>
              Normalmente, queremos <b>ler</b> uma entrada inserida pelo usuário
              e <b>escrever</b> uma saída na tela do computador:
            </p>
            <img
              src="@/assets/concepts_input_output.png"
              alt="exemplo de entrada e saída"
              class="mt-3"
              style="height: 70%; width: 70%; margin-left: 6rem"
            />
          </div>
          <div v-if="concept == 'operators'" class="definition">
            <p class="dialog-fuzzy dialog-sub-title mb-4">Operadores</p>
            <p>
              Em computação, temos os
              <span class="dialog-fuzzy">operadores aritméticos</span>, como na
              matemática, que podem operar números ou variáveis que armazenam
              números:
            </p>
            <img
              src="@/assets/concepts_operators_arithmetic.png"
              alt="exemplo de operadores aritméticos"
              class="mt-3"
              style="height: 70%; width: 70%; margin-left: 8rem"
            />

            <p class="mt-3">
              Outra operação muito utilizada é a comparação entre duas
              expressões, a qual tem como resultado um valor verdadeiro ou
              falso. Os
              <span class="dialog-fuzzy">operadores de comparação</span> são:
            </p>
            <img
              src="@/assets/concepts_operators_comparison.png"
              alt="exemplo de operadores de comparação"
              class="mt-3"
              style="height: 70%; width: 70%; margin-left: 8rem"
            />
            <p class="mt-3">
              Obs. Em linguagens de programação, é comum a sintaxe x == y para a
              comparação de igual e x != y para a comparação de diferença.
            </p>

            <p class="mt-3">
              Além disso, também temos os
              <span class="dialog-fuzzy">operadores lógicos</span>, que podem
              ser usados para criar expressões condicionais complexas.
            </p>
            <img
              src="@/assets/concepts_operators_logic.png"
              alt="exemplo de operadores lógicos"
              class="mt-3"
              style="height: 80%; width: 80%; margin-left: 4rem"
            />
          </div>
          <div v-if="concept == 'conditional'" class="definition">
            <p class="dialog-fuzzy dialog-sub-title mb-4">Condicional</p>
            <p>
              Representa uma condição no algoritmo, que pode levar a diferentes
              execuções de tarefas, caso ela seja verdadeira ou falsa.
            </p>
            <img
              src="@/assets/concepts_conditional.png"
              alt="exemplo de condicional"
              class="mt-3"
              style="height: 90%; width: 90%; margin-left: 2rem"
            />
          </div>
          <div v-if="concept == 'loop'" class="definition">
            <p class="dialog-fuzzy dialog-sub-title mb-4">Laço de repetição</p>
            <p>
              Representa a repetição da execução de tarefas <b>enquanto</b> uma
              determinada condição seja verdadeira. Assim, o algoritmo só para
              de executar quando a condição for falsa.
            </p>
            <img
              src="@/assets/concepts_loop.png"
              alt="exemplo de laço de repetição"
              class="mt-3"
              style="height: 70%; width: 70%; margin-left: 6rem"
            />
            <p class="mt-3">
              Observe que se a condição for sempre verdadeira, então as tarefas
              dentro do bloco serão executadas infinitamente! Em computação,
              isso é chamado de <span class="dialog-fuzzy">loop infinito</span>.
              Eles devem ser evitados no código.
            </p>
          </div>
        </v-col>
      </v-row>

      <v-card-actions>
        <v-btn :text="buttonText" @click="close"></v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data: () => ({
    concept: "pseudocode",
  }),
  props: {
    openDialog: { type: Boolean, required: true },
    buttonText: { type: String, required: true },
  },
  methods: {
    close() {
      this.$emit("closeDialog", false);
    },
  },
});
</script>

<style>
.dialog-title {
  font-size: 1.5rem;
  text-align: center;
  background-color: #86c5e1;
  border-radius: 1rem;
  padding: 0.2rem;
  margin: 1rem;
}

.dialog-sub-title {
  text-align: center;
  background-color: #e9e8e8;
  border-radius: 1rem;
  padding: 0.4rem 0.8rem;
  margin-left: -0.4rem;
}

.dialog-fuzzy {
  font-family: "Fuzzy Bubbles", sans-serif;
  color: #1d2d44;
}

.side-menu {
  cursor: pointer;
}

.definition {
  padding: 0.5rem 2rem;
}
</style>
