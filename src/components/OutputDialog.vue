<template>
  <v-dialog v-model="openOutputDialog" width="300px">
    <v-card :text="content">
      <v-card-actions>
        <v-btn text="Começar" @click="close"></v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    openOutputDialog: { type: Boolean, required: true },
    content: { type: String, required: true },
  },
  methods: {
    close() {
      this.$emit("closeOutputDialog", false);
    },
  },
});
</script>
