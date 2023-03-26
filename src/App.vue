<template>
  <div class="page">
    <main class="content">
      <div v-for="(item, index) in stopwatches" :key="index">
        <Stopwatch />
      </div>
      <div class="add-button-container">
        <button @click="addStopwatch" class="button add-button"></button>
      </div>
    </main>
  </div>
</template>

<script>
import { reactive } from 'vue';
import Stopwatch from './components/Stopwatch-item.vue';

export default {
  name: 'App',
  components: {
    Stopwatch,
  },
  data() {
    const stopwatches = reactive([{}]);
    const addStopwatch = () => {
      stopwatches.push({});
    };
    return {
      stopwatches,
      addStopwatch,
    };
  },
};
</script>

<style>
@import url(./assets/vendor/normalize.css);
@import url(./assets/vendor/fonts/fonts.css);

#app {
  font-family: 'Inter', 'Arial', sans-serif;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
  -moz-text-size-adjust: 100%;
  text-rendering: optimizeLegibility;
  text-align: center;
  color: #9E9E9E;
  box-sizing: border-box;
}

.page {
  min-height: 100vh;
  background-color: #353638;
  margin: 0 auto;
}

.content {
  margin: 0 auto;
  padding: 72px 212px;
  max-width: 1200px;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(3, 225px);
  gap: 50px;
}

.button {
  width: 20px;
  height: 20px;
  background-position: center;
  background-repeat: no-repeat;
  background-color: transparent;
  padding: 0;
  border: unset;
  cursor: pointer;
  transition: opacity .9s;
}

.button:hover {
  opacity: .5;
  transition: opacity .3s;
}

.add-button-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 225px;
  height: 120px;
  background-color: #696969;
}

.add-button {
  background-image: url(./assets/images/add.svg);
}

@media screen and (max-width: 1023px) {
  .content {
    padding: 72px 135px;
    flex-wrap: wrap;
    grid-template-columns: repeat(2, 225px);
  }
}

@media screen and (max-width: 767px) {
  .content {
    padding: 72px 46px;
    grid-template-columns: 225px;
  }
}
</style>
