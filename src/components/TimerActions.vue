<template>
  <v-row>
    <v-col cols="6" class="text-center">
      <v-btn text @click="toggleTimer">
        <v-icon large class="mr-2">
          {{ playPauseIcon }}
        </v-icon>
        {{ playPauseText }}
      </v-btn>
    </v-col>
    <v-col cols="6" class="text-center">
      <v-btn text @click="stopTimer">
        <v-icon large class="mr-2">
          {{ iconStop }}
        </v-icon>
        Stop
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
  import { mdiPauseCircleOutline, mdiPlayCircleOutline, mdiStopCircleOutline } from '@mdi/js';

  export default {
    name: "TimerActions",
    props: {
      timerRunning: {
        type: Boolean,
        required: true,
      }
    },
    data: () => ({
      iconPause: mdiPauseCircleOutline,
      iconPlay: mdiPlayCircleOutline,
      iconStop: mdiStopCircleOutline,
    }),
    computed: {
      playPauseIcon() {
        return this.timerRunning ? this.iconPause : this.iconPlay
      },
      playPauseText() {
        return this.timerRunning ? 'Pause' : 'Play'
      }
    },
    methods: {
      stopTimer() {
        this.$emit('stopTimer');
      },
      toggleTimer() {
        if (this.timerRunning) {
          this.$emit('pauseTimer');
        } else {
          this.$emit('playTimer');
        }
      }
    }
  }
</script>

<style scoped>

</style>
