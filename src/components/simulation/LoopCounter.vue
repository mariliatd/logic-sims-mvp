<template>
  <div v-if="selectedItem == 'birthday_cake'" id="bake-cake">
    <img
      src="@/assets/bake.svg"
      alt="fogão"
      width="200px"
      height="200px"
      @click="incrementCounter()"
      class="counter-increment"
    />
    <div v-for="index in totalPrepared" :key="index" id="cake-prepared">
      <img
        src="@/assets/birthday-cake.svg"
        alt="bolo de aniversário"
        width="100px"
        height="100px"
      />
    </div>
  </div>
  <div v-if="selectedItem == 'balloon'">
    <div>
      <img
        src="@/assets/gas-cylinder.svg"
        alt="cilindro de gás"
        width="200px"
        height="200px"
        @click="incrementCounter()"
        class="counter-increment"
      />
    </div>
    <div id="balloon-box">
      <div v-for="index in totalPrepared" :key="index" id="balloon-prepared">
        <img
          src="@/assets/balloon.svg"
          alt="balão"
          width="100px"
          height="100px"
        />
      </div>
    </div>
  </div>
  <div v-if="selectedItem == 'party_candy'" id="plate-candy-box">
    <div>
      <img
        src="@/assets/plate.svg"
        alt="prato"
        width="250px"
        height="200px"
        @click="incrementCounter()"
        class="counter-increment"
      />
      <img
        src="@/assets/plate.svg"
        alt="prato"
        width="250px"
        height="200px"
        style="margin-left: -3rem"
        @click="incrementCounter()"
        class="counter-increment"
      />
    </div>
    <div id="candy-box">
      <div v-for="index in totalPrepared" :key="index" id="candy-prepared">
        <img
          src="@/assets/party-candy.svg"
          alt="doce de festa"
          width="50px"
          height="50px"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    selectedItem: { type: String, required: true },
    total: { type: Number, required: true },
    totalPrepared: { type: Number, required: true },
  },
  data: () => ({
    count: 0,
  }),
  methods: {
    incrementCounter() {
      if (this.count < this.total) {
        this.count++;
      }
      this.$emit("totalPrepared", this.count);
    },
  },
});
</script>

<style>
.counter-increment {
  cursor: pointer;
}

#bake-cake {
  display: flex;
}

#cake-prepared {
  align-self: flex-start;
  margin-left: 25%;
}

#balloon-box {
  margin-left: 25%;
  display: flex;
  flex-wrap: wrap;
  width: 50%;
  height: 0;
  gap: 6rem 0;
  justify-content: center;
}

#balloon-prepared {
  align-self: flex-start;
  margin-top: -20rem;
  margin-left: -2rem;
}

#plate-candy-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

#candy-box {
  display: flex;
  justify-content: center;
}

#candy-prepared {
  align-self: flex-start;
  margin-top: -11.3rem;
  margin-left: -2rem;
}
</style>
