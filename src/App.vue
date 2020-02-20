<template>
  <v-app>
    <v-content>
      <Timer />
    </v-content>
  </v-app>
</template>

<script>
import Timer from './components/Timer';

export default {
  name: 'App',

  components: {
    Timer,
  },

  data: () => ({}),
};
</script>

<style scoped>
  #app {
    background: url('https://source.unsplash.com/1600x900/?disney') no-repeat center center/cover;
  }
</style>
