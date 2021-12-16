<template>
  <div id="app">
    <h1>SET SCHEDULE</h1>
    <div class="app__time-line">
      <h6 class="app__text">ALL <br> DAY</h6>
      <div class="app__time">
        <div class="app__time-wrap">
          <span class="app__time-text">00:00</span>
          <span class="app__time-text">03:00</span>
          <span class="app__time-text">06:00</span>
          <span class="app__time-text">09:00</span>
          <span class="app__time-text">12:00</span>
          <span class="app__time-text">15:00</span>
          <span class="app__time-text">18:00</span>
          <span class="app__time-text">21:00</span>
        </div>
        <div class="app__time-wrap">
          <div class="app__strip"></div>
          <div class="app__strip"></div>
          <div class="app__strip"></div>
          <div class="app__strip"></div>
          <div class="app__strip"></div>
          <div class="app__strip"></div>
          <div class="app__strip"></div>
          <div class="app__strip"></div>
        </div>
      </div>
    </div>
    <vDay
        v-for="(daySchedule, dayName) in weekSchedule"
        :daySchedule="daySchedule"
        :dayName="dayName"
        :key="dayName"/>
  </div>
</template>

<script>
import VDay from "@/components/v-DayItem";

export default {
  name: 'App',
  components: {
    VDay
  },
  data() {
    return {
      weekSchedule: {
        "mo": [
          {
            "bt": 240,
            "et": 779
          }
        ],
        "tu": [],
        "we": [],
        "th": [
          {
            "bt": 240,
            "et": 779
          },
          {
            "bt": 1140,
            "et": 1319
          }
        ],
        "fr": [
          {
            "bt": 660,
            "et": 1019
          }
        ],
        "sa": [
          {
            "bt": 0,
            "et": 1439
          }
        ],
        "su": []
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  box-sizing: border-box;
  width: 1496px;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;


}

h1 {
  margin-top: 50px;
  margin-bottom: 100px;
}

.app__time-line {
  display: flex;
  align-items: center;
  width: 1348px;
  position: absolute;
  right: -5px;
  top: 94px;
  z-index: -2;
}

.app__time-wrap {
  display: flex;
  align-items: center;
  width: 1248px;
  margin-left: 32px;
}

.app__text {
  font-size: 20px;
  grid-row: 1/3;
  padding-bottom: 10px;
}

.app__strip {
  height: 20px;
  width: 2px;
  background: gray;
  margin-right: 153.7px;
}

.app__time-text {
  margin-right: 115px;
}
</style>
