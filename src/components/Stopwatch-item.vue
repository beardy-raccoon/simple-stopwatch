<template>
  <div :class="`stopwatch-container stopwatch-container${stopwatchState}`">
    <div :class="`timetable timetable${stopwatchState}`">
      <div class="timetable__container">
        <p v-if="time >= 3600" class="timetable__time">{{ getHours }}</p>
        <span v-if="time >= 3600">:</span>
        <p v-if="time >= 60" class="timetable__time">{{ getMinutes }}</p>
        <span v-if="time >= 60">:</span>
        <p v-if="time > 0" class="timetable__time">{{ getSeconds }}</p>
        <p v-else class="timetable__time">{{ time }}</p>
      </div>
    </div>
    <div class="timetable__buttons">
      <button v-if="!isRunnig" @click="start" class="button start-btn"></button>
      <button v-else @click="stop" :class="`button stop-btn${stopwatchState}`"></button>
      <button @click="reset" :class="`button reset-btn${stopwatchState}`"></button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      time: 0,
      isRunnig: false,
      interval: null,
    };
  },
  computed: {
    stopwatchState() {
      if (this.isRunnig) return '_active';
      return '';
    },
    getHours() {
      const hours = parseInt(this.time / 3600, 10);
      return hours < 10 ? `0${hours}` : hours;
    },
    getMinutes() {
      const minutes = parseInt(this.time / 60, 10) % 60;
      return minutes < 10 ? `0${minutes}` : minutes;
    },
    getSeconds() {
      const seconds = this.time % 60;
      return seconds < 10 ? `0${seconds}` : seconds;
    },
  },
  methods: {
    start() {
      this.isRunnig = true;
      this.interval = setInterval(() => { this.time += 1; }, 100);
    },
    stop() {
      this.isRunnig = false;
      clearInterval(this.interval);
    },
    reset() {
      this.isRunnig = false;
      clearInterval(this.interval);
      this.time = 0;
    },
  },
};
</script>

<style scoped>
.stopwatch-container {
  min-width: 225px;
  height: 120px;
  background-color: #696969;
  display: flex;
  flex-direction: column;
}

.stopwatch-container_active {
  color: #fff;
}

.timetable {
  width: 100%;
  min-height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 1px solid #9E9E9E;
}

.timetable_active {
  border-color: #fff;
}

.timetable__container {
  min-width: 99px;
  display: flex;
  justify-content: center;
}

.timetable__time {
  font-family: 'Gotham Pro';
  font-style: normal;
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  min-width: 30px;
  text-align: center;
  margin: 0;
}

.timetable__buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 60px;
  gap: 52px;
}

.start-btn {
  background-image: url(../assets/images/start.svg);
}

.stop-btn {
  background-image: url(../assets/images/stop.svg);
}

.stop-btn_active {
  background-image: url(../assets/images/stop-active.svg);
}

.reset-btn {
  background-image: url(../assets/images/reset.svg);
}

.reset-btn_active {
  background-image: url(../assets/images/reset-active.svg);
}
</style>
