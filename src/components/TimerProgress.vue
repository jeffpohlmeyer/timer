<template>
  <v-progress-circular
    color="white"
    size="300"
    width="10"
    :value="pctRemaining"
    rotate="-90"
  >
    <span id="minutes">{{ minutes }}:{{ seconds }} left</span>
  </v-progress-circular>
</template>

<script>
  export default {
    name: "TimerProgress",
    props: {
      timeRemaining: {
        type: Number,
        required: true
      },
      totalTime: {
        type: Number,
        required: true
      }
    },
    computed: {
      pctRemaining() {
        return (this.timeRemaining / (this.totalTime * 60)) * 100;
      },
      minutes() {
        return ('0' + Math.floor(this.timeRemaining / 60)).slice(-2);
      },
      seconds() {
        return ('0' + this.timeRemaining % 60).slice(-2);
      }
    }
  }
</script>

<style scoped>
  #minutes {
    font-size: 2rem;
  }
</style>
