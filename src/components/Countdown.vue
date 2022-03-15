<template>
  <div id="countdown-container">
    <label for="timeinput">Starting Time</label>
    <input
      @input="inputTime"
      v-model="startTime"
      id="timeinput"
      type="number"
    />
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
    <button v-if="active && counter > 0" @click="stopTimer()">Stop</button>
    <button v-else-if="counter > 0" @click="startTimer()">Start</button>
    <button @click="clear()">Clear</button>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'CountdownTimer',
  data() {
    return {
      active: false,
      counter: 131696789,
      startTime: 131696789,
      remainder: 0,
      animationFrame: 0,
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
      this.remainder = performance.now() - (this.startTime - this.counter);
      this.timerLoop();
    },
    timerLoop() {
      this.counter > 0
        ? (this.counter = this.startTime - (performance.now() - this.remainder))
        : ((this.counter = 0), cancelAnimationFrame(this.animationFrame));
      this.animationFrame = requestAnimationFrame(this.timerLoop);
    },
    stopTimer() {
      this.active = false;
      cancelAnimationFrame(this.animationFrame);
    },
    inputTime() {
      this.active ? this.clear() : (this.counter = this.startTime);
    },
    clear() {
      this.counter = this.startTime;
      this.remainder = 0;
      this.stopTimer();
      this.animationFrame = 0;
    },
  },
};
</script>

<style scoped>
#countdown-container {
  border-bottom: 0.05rem solid darkgray;
  padding: 1.2rem 0 2.5rem;
}

label {
  font-size: 0.8rem;
  position: absolute;
  transform: translateY(-18px);
}

input {
  border: 0.05rem solid lightgray;
  padding: 2px 6px;
  width: 180px;
  border-radius: 0.8rem;
  transition: all 200ms ease;
}

input:focus {
  outline: none;
  border-bottom: 0.1rem solid #3399ff;
}
</style>
