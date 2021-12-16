<template>
  <div class="v-day">
    <div
        class="v-day__name"
        :class="{'active' : daySchedule.length}"
    >
      {{ dayName.toUpperCase() }}
    </div>
    <button
        class="v-day__button"
        :class="{'active-button' : activeButton}"
        @click="selectDay">
      &#10004;
    </button>
    <div class="v-day__hours">
      <VHour
          v-for="(hour,index) of hours"
          :key="index"
          :hour="hour"
          @selectHour="selectHour"
          @clearHour="clearHour"
      />
    </div>
  </div>
</template>

<script>
import VHour from "@/components/v-HourItem";

export default {
  name: "v-Day",
  components: {VHour},
  props: {
    dayName: {
      type: String,
      required: true
    },
    daySchedule: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      hours: [           // for render hours
        {
          start: 0,
          end: 59,
          select: false
        },
        {
          start: 60,
          end: 119,
          select: false
        },
        {
          start: 120,
          end: 179,
          select: false
        },
        {
          start: 180,
          end: 239,
          select: false
        },
        {
          start: 240,
          end: 299,
          select: false
        },
        {
          start: 300,
          end: 359,
          select: false
        },
        {
          start: 360,
          end: 419,
          select: false
        },
        {
          start: 420,
          end: 479,
          select: false
        },
        {
          start: 480,
          end: 539,
          select: false
        },
        {
          start: 540,
          end: 599,
          select: false
        },
        {
          start: 600,
          end: 659,
          select: false
        },
        {
          start: 660,
          end: 719,
          select: false
        },
        {
          start: 720,
          end: 779,
          select: false
        },
        {
          start: 780,
          end: 839,
          select: false
        },
        {
          start: 840,
          end: 899,
          select: false
        },
        {
          start: 900,
          end: 959,
          select: false
        },
        {
          start: 960,
          end: 1019,
          select: false
        },
        {
          start: 1020,
          end: 1079,
          select: false
        },
        {
          start: 1080,
          end: 1139,
          select: false
        },
        {
          start: 1140,
          end: 1199,
          select: false
        },
        {
          start: 1200,
          end: 1259,
          select: false
        },
        {
          start: 1260,
          end: 1319,
          select: false
        },
        {
          start: 1320,
          end: 1379,
          select: false
        },
        {
          start: 1380,
          end: 1439,
          select: false
        }
      ],
    }
  },
  computed: {
    activeButton() {
      return this.daySchedule[0]?.bt === 0 && this.daySchedule[0]?.et === 1439
    },
  },
  methods: {
    clearHour(start, end) {
      for (let index in this.daySchedule) {
        if (this.daySchedule[index].bt === start && this.daySchedule[index].et === end) {
          this.daySchedule.splice(+index, 1)
        } else if (this.daySchedule[index].bt === start) {
          this.daySchedule[index].bt = end + 1
        } else if (this.daySchedule[index].et === end) {
          this.daySchedule[index].et = start - 1
        } else if (this.daySchedule[index].bt < start && this.daySchedule[index].et > end) {
          this.daySchedule.push({
            "bt": this.daySchedule[index].bt,
            "et": start - 1
          })
          this.daySchedule.push({
            "bt": end + 1,
            "et": this.daySchedule[index].et
          })
          this.daySchedule.splice(+index, 1)
          this.addClass()
        }
      }
      this.addClass()
    },
    selectHour(start, end) {
      for (let obj of this.daySchedule) {
        if (obj.bt === end + 1) {
          obj.bt = start
          this.uniteHours()
          this.addClass()
          return
        } else if (obj.et === start - 1) {
          obj.et = end
          this.uniteHours()
          this.addClass()
          return
        } else if (obj.et <= end && obj.bt >= start) {
          return
        }
      }
      this.daySchedule.push({
        "bt": start,
        "et": end
      })
      this.addClass()
    },
    uniteHours() {
      for (let i = this.daySchedule.length - 1; i > 0; i--) {
        let newObj = this.daySchedule[i]
        this.daySchedule.splice(i, 1)
        this.selectHour(newObj?.bt, newObj?.et)
      }
    },
    addClass() {
      for (let hour of this.hours) {
        this.daySchedule.find(obj => obj.bt <= hour.start && obj.et >= hour.end) ? hour.select = true : hour.select = false
      }
    },
    selectDay() {
      if (this.daySchedule[0]?.bt === 0) {
        this.daySchedule.splice(0, this.daySchedule.length)
        this.addClass()
      } else {
        this.daySchedule.splice(0, this.daySchedule.length)
        this.daySchedule.push({
          "bt": 0,
          "et": 1439
        })
        this.addClass()
      }
    }
  }
  ,
  mounted() {
    this.addClass()
  }
}
</script>

<style scoped>
.v-day {
  display: flex;
  width: fit-content;
}

.v-day__name {
  height: 100px;
  width: 100px;
  color: black;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid gray;
}

.active {
  background: lightgray
}

.v-day__button {
  background: #2c3e50;
  height: 102px;
  width: 100px;
  border: 1px solid gray;
  font-size: 30px;
  color: #2c3e50;
}
.active-button{
  color: azure;
}

.v-day__hours {
  display: flex;
}

</style>