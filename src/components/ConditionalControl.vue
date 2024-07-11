<template>
  <div class="control-box">
    <p class="label-text">{{ label }}</p>
    <div class="control">
      <v-row>
        <v-col v-for="item in content" :key="item.name" :cols="item.size">
          <div class="item-box choosen-item" @click="choosenItem = item.name">
            <img :src="item.path" :alt="item.text" width="80px" height="80px" />
            <p class="item-label">{{ item.label }}</p>
          </div>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script lang="ts">
import type { ConditionalCard } from "@/types";
import { defineComponent, type PropType } from "vue";

export default defineComponent({
  props: {
    label: { type: String, required: true },
    content: {
      type: Array as PropType<Array<ConditionalCard>>,
      require: true,
      default: () => [],
    },
  },
  data: () => ({
    choosenItem: "",
  }),
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
  margin-bottom: 0.2rem;
}

.control {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  background-color: #e9e8e8;
  width: 350px;
  height: 150px;
  display: flex;
  align-items: center;
}

.choosen-item {
  cursor: pointer;
}

.choosen-item:hover {
  background-color: #d9d9d9;
  border-radius: 1rem;
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
