<template>
  <div class="counter-box">
    <p class="label-text">{{ label }}</p>
    <div class="counter">
      <v-btn
        variant="text"
        style="min-width: 0; left: 0.5rem; margin-right: 0.5rem; padding: 0"
        @click="incrementCounter()"
      >
        <v-icon icon="mdi-plus-box-outline" size="35px"></v-icon>
      </v-btn>
      <span class="text">{{ count }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    label: { type: String, required: true },
    total: { type: Number, required: true },
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
.counter-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.label-text {
  text-align: center;
  margin-bottom: 0.2rem;
}

.counter {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  background-color: #e9e8e8;
  width: 100px;
  height: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.text {
  font-size: 1.8rem;
  text-align: center;
  padding: 0.5rem 0.7rem;
}
</style>
