<template>
  <div id="app">
    <h3>Stopwatch:</h3>
    <StopWatch />
    <h3>Countdown Timer:</h3>
    <CountdownTimer />
  </div>
</template>

<script>
import CountdownTimer from './components/Countdown.vue';
import StopWatch from './components/Stopwatch.vue';

export default {
  name: 'App',
  components: {
    CountdownTimer,
    StopWatch,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

#app {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}

#timer-display {
  padding: 1.2rem 0;
}

#timer-label {
  margin: auto;
  width: 8.3rem;
  display: flex;
  justify-content: space-between;
}

h4 {
  margin: 0;
}

span {
  font-size: 0.7rem;
}

button {
  background: transparent;
  margin: 0 4px;
  padding: 0.4rem 1rem;
  cursor: pointer;
  border: 0.05rem solid gray;
  border-radius: 0.5rem;
}
</style>
