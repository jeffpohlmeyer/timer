<template>
  <v-row align="end">
    <v-col cols="12">
      <v-subheader>Choose timer amount (minutes)</v-subheader>
      <v-slider
        v-model="minutes"
        :prepend-icon="iconTimer"
        thumb-label
        min="0"
        max="120"
        step="0.01"
        hide-details
        thumb-color="secondary"
      >
        <template v-slot:append>
          <v-text-field
            v-model="minutes"
            class="mt-0 pt-0"
            hide-details
            single-line
            type="number"
            style="width: 60px"
          />
        </template>
      </v-slider>
      <v-btn
        class="mt-5"
        block
        outlined
        @click="submitTimer"
      >
        Start Timer
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
  import { mdiTimer } from '@mdi/js';

  export default {
    name: "TimerForm",
    data: () => ({
      minutes: 1,
      iconTimer: mdiTimer
    }),
    methods: {
      submitTimer(){
        this.$emit('submitTimer', +this.minutes);
      }
    }
  }
</script>

<style scoped>

</style>
