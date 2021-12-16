<template>
  <div class="v-Hour"
       :class="{'v-Hour__select': hour.select}"
       @click="changeStatusHour"
       @mousemove="selectHour"
  >
  </div>
</template>

<script>
export default {
  name: "v-Hours",
  props: {
    hour: {
      type: Object,
      required: true
    },
    index: {
      type: Number
    }
  },
  methods: {
    selectHour(event) {
      if (event.buttons === 1) {
        if (!this.hour.select) {
          this.$emit('selectHour', this.hour.start, this.hour.end)
        }
      }
    },
    changeStatusHour() {
      if (this.hour.select) {
        this.$emit('clearHour', this.hour.start, this.hour.end, this.index)
      } else {
        this.$emit('selectHour', this.hour.start, this.hour.end)
      }
    }
  },
}
</script>
<style scoped>
.v-Hour {
  height: 100px;
  width: 50px;
  border: 1px solid gray;
}

.v-Hour__select {
  background: #2c3e50;
}
</style>