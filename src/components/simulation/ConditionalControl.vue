<template>
  <div class="control-box">
    <p class="label-text">{{ itemLabel }}</p>
    <div class="item-control">
      <v-row>
        <v-col v-for="item in content" :key="item.name" :cols="item.size">
          <button @click="selectItem(item)" :disabled="isDisabled(item.name)">
            <img :src="`${base}assets/${item.path}`" :alt="item.text" />
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
import type { ItemCard } from "@/types.ts";
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
    preparedItemList: { type: Array<String>, required: true },
  },
  methods: {
    selectItem(item: ItemCard) {
      this.$emit("selectedItem", item.name);
    },
    isDisabled(item: String) {
      return (
        (this.selectedItem !== "" && item !== this.selectedItem) ||
        this.preparedItemList.includes(item)
      );
    },
  },
});
</script>

<script setup lang="ts">
const base = import.meta.env.BASE_URL;
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

img {
  width: 80px;
  height: 80px;
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

@media screen and (min-width: 360px) and (max-width: 1080px) {
  .item-control {
    border: solid 0.12rem #1d2d44;
    border-radius: 1rem;
    background-color: #e9e8e8;
    width: 200px;
    height: 70px;
    display: flex;
    align-items: center;
    padding: 0 0.5rem;
    margin-bottom: 0.5rem;
  }

  img {
    width: 35px;
    height: 35px;
  }

  .amount-control {
    width: 200px;
    height: 40px;
    padding: 0 0.5rem;
  }
}
</style>
