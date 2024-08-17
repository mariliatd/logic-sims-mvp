<template>
  <v-dialog v-model="openOutputDialog" width="400px">
    <v-card :text="content">
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
    openOutputDialog: { type: Boolean, required: true },
    buttonText: { type: String, required: true },
    content: { type: String, required: true },
  },
  methods: {
    close() {
      this.$emit("closeOutputDialog", false);
    },
  },
});
</script>
