<template>
  <div class="template-box">
    <v-app>
      <v-row>
        <v-col cols="7" md="8">
          <div class="sim-box">
            <div class="sim-workspace">
              <slot name="workspace"></slot>
            </div>
            <div class="restore-sim">
              <v-icon
                icon="mdi-restore"
                size="60px"
                @click="restoreSim()"
              ></v-icon>
            </div>
          </div>
        </v-col>
        <v-col cols="5" md="4">
          <div class="code-box">
            <p class="sub-title">Pseudocódigo</p>
            <slot name="pseudocode"></slot>
          </div>
        </v-col>
      </v-row>
    </v-app>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  methods: {
    restoreSim() {
      this.$emit("sim");
    },
  },
});
</script>

<style>
.template-box {
  position: absolute;
  top: 4.7rem;
  bottom: 1.2rem;
  left: 1.2rem;
  right: 1.2rem;
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  overflow: hidden;
}

.sim-box {
  display: flex;
  flex-direction: column;
  margin: 1.2rem;
}

.restore-sim {
  position: fixed;
  bottom: 6rem;
  align-self: flex-end;
}

.code-box {
  font-size: 1.2rem;
  border: solid 0.12rem #1d2d44;
  border-radius: 1rem;
  margin: 1.2rem;
  padding-bottom: 0.2rem;
}

.sub-title {
  font-size: 1.4rem;
  text-align: center;
  background-color: #eccbdf;
  border-radius: 1rem;
  padding: 0.2rem;
  margin: 0.6rem;
}

@media screen and (min-width: 360px) and (max-width: 1080px) {
  .template-box {
    top: 4.5rem;
    bottom: 0.8rem;
    left: 0.8rem;
    right: 0.8rem;
    overflow: auto;
  }

  .sim-box {
    margin: 0.6rem;
  }

  .restore-sim {
    position: absolute;
    bottom: -16rem;
    align-self: flex-end;
  }

  .code-box {
    font-size: 1rem;
    margin: 0.6rem;
  }

  .sub-title {
    font-size: 1rem;
    padding: 0.2rem;
    margin: 0.4rem;
  }
}
</style>
