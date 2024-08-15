<template>
  <div class="control-box">
    <p class="label-text">{{ itemLabel }}</p>
    <div class="item-control">
      <v-row>
        <v-col v-for="item in content" :key="item.name" :cols="item.size">
          <button
            @click="selectItem(item)"
            :disabled="selectedItem !== '' && item.name !== selectedItem"
          >
            <img :src="item.path" :alt="item.text" width="80px" height="80px" />
          </button>
        </v-col>
      </v-row>
    </div>

    <p class="label-text">{{ amountLabel }}</p>
    <div class="amount-control">
      <v-row>
        <v-col v-for="item in content" :key="item.name" :cols="item.size">
          <p class="item-label">{{ item.label }}</p>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script lang="ts">
import type { ItemCard } from "@/types";
import { defineComponent, type PropType } from "vue";

export default defineComponent({
  props: {
    itemLabel: { type: String, required: true },
    amountLabel: { type: String, required: true },
    content: {
      type: Array as PropType<Array<ItemCard>>,
      require: true,
      default: () => [],
    },
    selectedItem: { type: String, required: true },
  },
  methods: {
    selectItem(item: ItemCard) {
      this.$emit("selectedItem", item.name);
    },
  },
});
</script>

<style>
.control-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.label-text {
  text-align: center;
}

.item-control {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  background-color: #e9e8e8;
  width: 360px;
  height: 120px;
  display: flex;
  align-items: center;
  padding: 0 0.5rem;
  margin-bottom: 0.5rem;
}

.amount-control {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  background-color: #e9e8e8;
  width: 360px;
  height: 50px;
  display: flex;
  align-items: center;
  padding: 0 0.5rem;
}

button {
  padding: 0.5rem;
}

button:hover:enabled {
  background-color: #d9d9d9;
  border-radius: 1rem;
}

button:disabled {
  border-radius: 1rem;
  opacity: 0.5;
}

.item-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.item-label {
  text-align: center;
}
</style>
