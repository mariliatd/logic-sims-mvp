<template>
  <div v-if="selectedItem == 'birthday_cake'" id="bake-cake">
    <img
      src="@/assets/bake.svg"
      alt="fogão"
      @click="incrementCounter()"
      class="counter-increment"
      id="bake-img"
    />
    <div v-for="index in totalPrepared" :key="index" id="cake-prepared">
      <img
        src="@/assets/birthday-cake.svg"
        alt="bolo de aniversário"
        id="cake-img"
      />
    </div>
  </div>
  <div v-if="selectedItem == 'balloon'">
    <div>
      <img
        src="@/assets/gas-cylinder.svg"
        alt="cilindro de gás"
        @click="incrementCounter()"
        class="counter-increment"
        id="cylinder-img"
      />
    </div>
    <div id="balloon-box">
      <div v-for="index in totalPrepared" :key="index" id="balloon-prepared">
        <img src="@/assets/balloon.svg" alt="balão" id="balloon-img" />
      </div>
    </div>
  </div>
  <div v-if="selectedItem == 'party_candy'" id="plate-candy-box">
    <div>
      <img
        src="@/assets/plate.svg"
        alt="prato"
        @click="incrementCounter()"
        class="counter-increment plate-img"
        id="left-plate"
      />
      <img
        src="@/assets/plate.svg"
        alt="prato"
        @click="incrementCounter()"
        class="counter-increment plate-img"
        id="right-plate"
      />
    </div>
    <div id="candy-box">
      <div v-for="index in totalPrepared" :key="index" id="candy-prepared">
        <img
          src="@/assets/party-candy.svg"
          alt="doce de festa"
          id="candy-img"
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

#bake-img {
  width: 200px;
  height: 200px;
}

#cake-prepared {
  align-self: flex-start;
  margin-left: 25%;
}

#cake-img {
  width: 100px;
  height: 100px;
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

#cylinder-img {
  width: 200px;
  height: 200px;
}

#balloon-prepared {
  align-self: flex-start;
  margin-top: -20rem;
  margin-left: -2rem;
}

#balloon-img {
  width: 100px;
  height: 100px;
}

#plate-candy-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.plate-img {
  width: 250px;
  height: 200px;
}

#right-plate {
  margin-left: -3rem;
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

#candy-img {
  width: 50px;
  height: 50px;
}

@media screen and (min-width: 360px) and (max-width: 1080px) {
  #bake-img {
    width: 100px;
    height: 100px;
  }

  #cake-img {
    width: 50px;
    height: 50px;
  }

  #balloon-box {
    margin-left: 25%;
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    height: 0;
    gap: 4rem 0;
    justify-content: center;
  }

  #cylinder-img {
    width: 100px;
    height: 100px;
  }

  #balloon-img {
    width: 50px;
    height: 50px;
  }

  .plate-img {
    width: 125px;
    height: 100px;
  }

  #right-plate {
    margin-left: -14rem;
  }

  #candy-prepared {
    margin-top: -5.8rem;
    margin-left: -1rem;
  }

  #candy-img {
    width: 25px;
    height: 25px;
  }
}
</style>
