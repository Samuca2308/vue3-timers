<template>
  <div id="stopwatch-container">
    <div id="timer-display">
      <h4>{{ timerOutput }}</h4>
      <div id="timer-label">
        <span>d</span>
        <span>h</span>
        <span>m</span>
        <span>s</span>
        <span>ms</span>
      </div>
    </div>
    <button v-if="active" @click="stopTimer()">Stop</button>
    <button v-else @click="startTimer()">Start</button>
    <button @click="clear()">Clear</button>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'StopWatch',
  data() {
    return {
      active: false,
      animationFrame: 0,
      remainder: 0,
      counter: 0,
    };
  },
  computed: {
    timerOutput() {
      return moment()
        .days(0)
        .hours(0)
        .minutes(0)
        .seconds(0)
        .milliseconds(this.counter)
        .format('d : HH : mm : ss : SSS');
    },
  },
  methods: {
    startTimer() {
      this.active = true;
      this.remainder = Math.floor(moment.now() - this.counter);
      this.timerLoop();
    },
    timerLoop() {
      this.counter = moment.now() - this.remainder;
      this.animationFrame = requestAnimationFrame(this.timerLoop);
    },
    stopTimer() {
      this.active = false;
      cancelAnimationFrame(this.animationFrame);
    },
    clear() {
      this.remainder = 0;
      this.counter = 0;
      this.stopTimer();
      this.animationFrame = 0;
    },
  },
};
</script>

<style scoped>
#stopwatch-container {
  border-bottom: 0.05rem solid darkgray;
  padding-bottom: 2.5rem;
}
</style>
