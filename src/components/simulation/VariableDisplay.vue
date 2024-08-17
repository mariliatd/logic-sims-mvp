<template>
  <div class="variable">
    <p class="name">{{ name }}</p>
    <div class="value">
      <span :class="[isString(value) ? 'text' : 'number']">{{ value }}</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    name: { type: String, required: true },
    value: { type: [Number, String], required: true },
  },
  methods: {
    isString(value: number | string): boolean {
      return typeof value === "string";
    },
  },
});
</script>

<style>
.variable {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.name {
  text-align: center;
  margin-bottom: 0.2rem;
}

.value {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  background-color: #e9e8e8;
  width: 80px;
  height: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.text {
  font-size: 1.6rem;
}

.number {
  font-size: 1.8rem;
}
</style>
