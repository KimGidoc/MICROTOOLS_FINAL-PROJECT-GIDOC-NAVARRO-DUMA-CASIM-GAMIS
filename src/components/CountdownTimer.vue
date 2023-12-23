<template>
    <div class="col-md-8 p-5" v-if="showCountdownTimerComponent">
        <div class="text-center mb-5">
            <h1>Countdown Timer</h1>
        </div>
        <div class="form-group" v-if="!isRunning">
            <label style="font-weight: bold;">Timer Duration (in seconds):</label>
            <input type="number" id="duration" v-model="duration" min="1" :disabled="isRunning" class="form-control mt-2" placeholder="Input timer duration">
        </div>
        <div class="d-flex justify-content-center p-3">
            <div v-if="!isRunning">
                <button class="btn btn-warning m-1" @click="startTimer" :disabled="duration <= 0">Start Timer</button>
            </div>
            <div v-else>
                <button class="btn btn-danger m-1" @click="stopTimer">Stop Timer</button>
            </div>
        </div>

        <div v-if="isRunning" class="mt-3">
            <h5>Time Remaining:</h5>
            <H1 style="font-weight: bold; font-size: 60px" class="form-control text-center p-5" rows="1" readonly>
            {{ formatTime(remainingTime) }}</h1>
        </div>

    </div>
</template>


<script>
export default {
    props: ['showCountdownTimerComponent'],
  data() {
    return {
      duration: 60, // Initial duration in seconds
      isRunning: false,
      remainingTime: 0,
      intervalId: null,
    };
  },
  methods: {
    startTimer() {
      if (this.duration > 0 && !this.isRunning) {
        this.isRunning = true;
        this.remainingTime = this.duration;

        this.intervalId = setInterval(() => {
          if (this.remainingTime > 0) {
            this.remainingTime--;
          } else {
            this.stopTimer();
          }
        }, 1000);
      }
    },
    stopTimer() {
      clearInterval(this.intervalId);
      this.isRunning = false;
      this.remainingTime = 0;
    },
    formatTime(seconds) {
      const minutes = Math.floor(seconds / 60);
      const remainingSeconds = seconds % 60;
      return `${minutes}:${remainingSeconds < 10 ? '0' : ''}${remainingSeconds}`;
    },
  },
  beforeDestroy() {
    clearInterval(this.intervalId);
  },
};
</script>