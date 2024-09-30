<template>
  <v-dialog v-model="openDialog" @click:outside="close" width="1500px">
    <v-card>
      <p class="dialog-fuzzy dialog-title">Conceitos de Programação</p>
      <div class="definition">
        <p class="dialog-fuzzy mb-3">
          <span class="dialog-sub-title">O que é um pseudocódigo?</span>
        </p>
        <p>
          É uma forma de escrever um
          <span class="dialog-fuzzy">algoritmo</span> com uma linguagem simples,
          sem necessidade de conhecer uma linguagem de programação específica.
        </p>
        <p>
          Um <span class="dialog-fuzzy">algoritmo</span> é qualquer sequência
          finita de passos para resolver um problema ou completar tarefa. É como
          dizemos para um computador o que queremos que ele faça.
        </p>
        <p class="mt-3">Um exemplo de algoritmo é uma receita de bolo:</p>
        <ol class="ml-10">
          <li>Separar os ingredientes: açúcar, margarina, ovos, etc</li>
          <li>Bater o açúcar, a margarina e os ovos</li>
          <li>Acrescentar a farinha, o leite e o fermento em pó</li>
          <li>Untar a forma com farinha</li>
          <li>Assar o bolo a 180°C em forno pré-aquecido por 40 minutos</li>
        </ol>
      </div>

      <div class="definition">
        <p class="dialog-fuzzy mb-3">
          <span class="dialog-sub-title">Variáveis</span>
        </p>
        <p>
          São espaços na memória do computador que guardam algum dado ou
          informação. Esses valores armazenados podem ou não ser alterados ao
          longo do programa.
        </p>
        <p class="mt-3">Exemplos de variáveis:</p>
        <ul class="ml-10">
          <li>
            nome <v-icon icon="mdi-arrow-left" size="20px"></v-icon> "Maria"
          </li>
          <li>idade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10</li>
          <li>
            ingrediente1
            <v-icon icon="mdi-arrow-left" size="20px"></v-icon> "açúcar"
          </li>
        </ul>
      </div>

      <div class="definition">
        <p class="dialog-fuzzy mb-3">
          <span class="dialog-sub-title">Entrada e Saída</span>
        </p>
        <p>
          A entrada de um algoritmo é algum dado recebido pelo computador, que
          será processado para produzir um resultado, que será a saída do
          programa.
        </p>
        <p class="mt-3">
          Por exemplo, quando fazemos um bolo, a entrada são os ingredientes e a
          saída é o bolo pronto.
        </p>
        <p>
          Normalmente, queremos <b>ler</b> uma entrada inserida pelo usuário e
          <b>escrever</b> uma saída na tela do computador:
        </p>
        <ul class="ml-10">
          <li><b>leia</b> (nome)</li>
          <li><b>escreva</b> ("Olá, {nome}!")</li>
        </ul>
        <p class="mt-3">
          Observe que o comando <b>leia</b> do pseudocódigo espera que o usuário
          insira um dado para ser armazenado na variável <b>nome</b>. E
          esperamos que o comando <b>escreva</b> retorne a mensagem,
          substituindo a variável <b>nome</b> pelo dado armazenado nela.
        </p>
      </div>

      <div class="definition">
        <p class="dialog-fuzzy mb-3">
          <span class="dialog-sub-title">Operadores</span>
        </p>
        <p>
          Em computação, temos os
          <span class="dialog-fuzzy">operadores aritméticos</span>, como na
          matemática, que podem operar números ou variáveis que armazenam
          números:
        </p>
        <ul class="ml-10">
          <li>x + y (soma)</li>
          <p>
            Ex.: soma <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 1 + 1
            (2)
          </p>
          <p class="ml-10">
            novo_numero <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10 +
            soma (12, pois utilizamos a variável do exemplo anterior)
          </p>
          <li>x - y (subtração)</li>
          <p>
            Ex.: numero <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 5 -
            2 (3)
          </p>
          <li>x * y (multiplicação)</li>
          <p>
            Ex.: z <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 3 * 4
            (12)
          </p>
          <li>x / y (divisao)</li>
          <p>
            Ex.: metade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10 /
            2 (5)
          </p>
          <li>x % y (resto da divisão)</li>
          <p>
            Ex.: metade <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 10 %
            2 (0, pois ao dividir 10 por 2, o resto da divisão é 0)
          </p>
        </ul>

        <p class="mt-3">
          Outra operação muito utilizada é a comparação entre duas expressões, a
          qual tem como resultado um valor verdadeiro ou falso. Os
          <span class="dialog-fuzzy">operadores de comparação</span> são:
        </p>
        <ul class="ml-10">
          <li>x = y (x é igual a y)</li>
          Obs. Em linguagens de programação, é comum a sintaxe x == y para a
          comparação de igual.
          <li>x != y (x é diferente de y)</li>
          <li>x > y (x é maior do que y)</li>
          <li>x < y (x é menor do que y)</li>
          <li>x >= y (x é maior ou igual a y)</li>
          <li>x <= y (x é menor ou igual a y)</li>
        </ul>

        <p class="mt-3">
          Além disso, também temos os
          <span class="dialog-fuzzy">operadores lógicos</span>, que podem ser
          usados para criar expressões condicionais complexas.
        </p>
        <ul class="ml-10">
          <li><b>E</b> (conjunção):</li>
          <ul class="ml-5">
            <li>x > 0 <b>E</b> x < 10</li>
          </ul>
          <p>
            A operação só será verdadeira se as duas expressões forem
            verdadeiras.
          </p>
          <p>
            Por exemplo, se x
            <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 12, o resultado
            será falso e se x
            <v-icon icon="mdi-arrow-left" size="20px"></v-icon>5, o reultado é
            verdadeiro.
          </p>
        </ul>
        <ul class="ml-10">
          <li><b>OU</b> (disjunção):</li>
          <ul class="ml-5">
            <li>x > 0 <b>OU</b> x < 10</li>
          </ul>
          <p>
            A operação será verdadeira se uma das duas expressões forem
            verdadeiras.
          </p>
          <p>
            Por exemplo, se x
            <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 12, o resultado
            será verdadeiro e se x
            <v-icon icon="mdi-arrow-left" size="20px"></v-icon>5, o reultado
            também é verdadeiro.
          </p>
        </ul>
        <ul class="ml-10">
          <li><b>NÃO</b> (negação):</li>
          <ul class="ml-5">
            <li><b>NÃO</b> x > 0</li>
          </ul>
          <p>
            A operação torna o valor verdadeiro em falso e o falso em
            verdadeiro.
          </p>
          <p>
            Ou seja, se x
            <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 5, então x é
            maior do que 0 (verdadeiro) e o resultado da expressão será falso.
          </p>
        </ul>
      </div>

      <div class="definition">
        <p class="dialog-fuzzy mb-3">
          <span class="dialog-sub-title">Condicional</span>
        </p>
        <p>
          Representa uma condição no algoritmo, que pode levar a diferentes
          execuções de tarefas, caso ela seja verdadeira ou falsa.
        </p>
        <p class="mt-3">Por exemplo:</p>
        <p class="ml-7"><b>se</b> fizer sol hoje <b>então</b> vá à praia</p>
        <p class="ml-7"><b>senão</b> fique em casa e jogue videogame</p>

        <p class="mt-3">
          Observe que poderíamos ter apenas o caso em que a condição é
          verdadeira:
        </p>
        <p class="ml-7"><b>se</b> quero ir à praia <b>então</b> vou à praia</p>

        <p class="mt-3">
          Outro caso que podemos encontrar uma condição que leva a uma tarefa
          que é também uma condição:
        </p>
        <p class="ml-7"><b>se</b> fizer sol hoje <b>então</b> vá à praia</p>
        <p class="ml-7"><b>senão</b></p>
        <p class="ml-14">
          <b>se</b> o dia estiver nublado <b>então</b> vá ao cinema
        </p>
        <p class="ml-14"><b>senão</b> fique em casa e jogue videogame</p>
      </div>

      <div class="definition">
        <p class="dialog-fuzzy mb-3">
          <span class="dialog-sub-title">Laço de repetição</span>
        </p>
        <p>
          Representa a repetição da execução de tarefas <b>enquanto</b> uma
          determinada condição seja verdadeira. Assim, o algoritmo só para de
          executar quando a condição for falsa.
        </p>
        <p class="mt-3">Por exemplo:</p>
        <p class="ml-7"><b>escreva</b> ("Conte de 0 a 10.")</p>
        <p class="ml-7">
          contagem <v-icon icon="mdi-arrow-left" size="20px"></v-icon> 0
        </p>
        <p class="ml-7"><b>enquanto</b> contagem <= 10 <b>faça</b></p>
        <p class="ml-14"><b>escreva</b> ("{contagem}")</p>
        <p class="ml-14">
          contagem <v-icon icon="mdi-arrow-left" size="20px"></v-icon> contagem
          + 1
        </p>
        <p class="mt-3">
          Observe que se a condição for sempre verdadeira, então as tarefas
          dentro do bloco serão executadas infinitamente! Em computação, isso é
          chamado de <span class="dialog-fuzzy">loop infinito</span>. Eles devem
          ser evitados no código.
        </p>
      </div>
      <v-card-actions>
        <v-btn :text="buttonText" @click="close"></v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
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
  background-color: #e9e8e8;
  border-radius: 1rem;
  padding: 0.4rem 0.8rem;
  margin-left: -0.4rem;
}

.dialog-fuzzy {
  font-family: "Fuzzy Bubbles", sans-serif;
  color: #1d2d44;
}

.definition {
  padding: 1rem 2rem;
}
</style>
