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
          <TimerForm
            @submitTimer="submitTimer"
          />
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
  import TimerProgress from "./TimerProgress";
  import TimerForm from "./TimerForm";
  export default {
    name: "TimerBase",
    components: {TimerForm, TimerProgress},
    data: () => ({
      totalTime: 1,
      timeRemaining: 60,
      iter: 0,
      interval: null,
    }),
    methods: {
      submitTimer(payload) {
        clearInterval(this.interval);
        this.iter = 0;
        this.totalTime = payload;
        this.interval = setInterval(() => {
          this.iter += 1;
          this.timeRemaining = (this.totalTime * 60) - this.iter;
          if (this.timeRemaining === 0) clearInterval(this.interval);
        }, 1000)
      },
    }
  }
</script>

<style scoped>

</style>
