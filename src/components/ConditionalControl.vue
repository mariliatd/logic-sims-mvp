<template>
  <div class="control-box">
    <p class="label-text">{{ label }}</p>
    <div class="control">
      <v-row>
        <v-col v-for="card in content" :key="card.name" :cols="card.size">
          <v-card variant="text">
            <v-card-actions>
              <img
                :src="card.path"
                :alt="card.text"
                width="80px"
                height="80px"
                @click="choosenItem = card.name"
                class="card-img"
              />
            </v-card-actions>
            <p class="card-label">{{ card.label }}</p>
          </v-card>
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
  position: fixed;
}

.label-text {
  text-align: center;
  margin-bottom: 0.2rem;
}

.control {
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  width: 350px;
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card-img {
  cursor: pointer;
}

.card-label {
  text-align: center;
}
</style>
