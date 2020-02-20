<template>
  <v-row justify="center">
    <v-col cols="12" md="6">
      <v-card color="primary" dark>
        <v-card-title>
          Timer
        </v-card-title>
        <v-card-text class="text-center">
          <TimerProgress
            :time-remaining="timeRemaining"
            :total-time="totalTime"
          />
        </v-card-text>
        <v-divider />
        <v-card-actions>
          <TimerActions
            v-if="timerStarted"
            :timer-running="timerRunning"
            @stopTimer="stopTimer"
            @pauseTimer="pauseTimer"
            @playTimer="playTimer"
          />
          <TimerForm
            v-if="!timerStarted"
            @submitTimer="startTimer"
          />
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
  import TimerProgress from "./TimerProgress";
  import TimerForm from "./TimerForm";
  import TimerActions from "./TimerActions";

  export default {
    name: "TimerBase",
    components: {TimerForm, TimerProgress, TimerActions},
    data: () => ({
      totalTime: 1,
      timeRemaining: 60,
      iter: 0,
      interval: null,
      timerRunning: false,
      timerStarted: false,
    }),
    methods: {
      stopTimer() {
        clearInterval(this.interval);
        this.timeRemaining = this.totalTime * 60;
        this.timerStarted = false;
        this.timerRunning = false;
      },
      pauseTimer() {
        clearInterval(this.interval);
        this.timerRunning = false;
      },
      playTimer() {
        this.interval = setInterval(() => {
          this.iter += 1;
          this.timeRemaining = (this.totalTime * 60) - this.iter;
          if (this.timeRemaining === 0) clearInterval(this.interval);
        }, 1000);
        this.timerRunning = true;
      },
      startTimer(payload) {
        this.iter = 0;
        this.totalTime = payload;
        this.timerStarted = true;
        this.playTimer();
      },
    },
  }
</script>

<style scoped>

</style>
