<template>
  <div class="timer">
    <h1>{{ msg }}</h1>
    <h2>{{ formatted }}</h2>
    <button v-on:click="start()">start</button>
    <button v-on:click="stop()">stop</button>
    <button v-on:click="reset()">reset</button>
  </div>
</template>

<script>
export default {
  name: "Timer",
  props: {
    msg: String,
  },
  data() {
    return {
      min: 59,
      sec: 59,
      intervalId: 0,
    };
  },
  methods: {
    count() {
      if (this.sec <= 0 && this.min >= 1) {
        this.min--;
        this.sec = 59;
      } else if (this.sec <= 0 && this.min <= 0) {
        this.finish();
      } else {
        this.sec--;
      }
    },
    start() {
      if (this.intervalId > 0) {
        clearInterval(this.intervalId);
      }
      let self = this;
      this.intervalId = setInterval(() => {
        self.count();
      }, 1000);
    },
    stop() {
      clearInterval(this.intervalId);
    },
    reset() {
      if (this.intervalId > 0) {
        clearInterval(this.intervalId);
      }
      this.min = 59;
      this.sec = 59;
    },
    finish() {
      clearInterval(this.intervalId);
    },
  },
  computed: {
    formatted: function () {
      let minTime = this.min;
      let secTime = this.sec;
      if (minTime < 10 && secTime < 10) {
        return `0${minTime}:0${secTime}`;
      } else if (minTime >= 10 && secTime < 10) {
        return `${minTime}:0${secTime}`;
      } else if (minTime < 10 && secTime >= 10) {
        return `0${minTime}:${secTime}`;
      } else {
        return `${minTime}:${secTime}`;
      }
    },
  },
};
</script>

<style scoped>
</style>
