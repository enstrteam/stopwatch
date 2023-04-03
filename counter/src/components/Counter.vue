<template>
  <div class="counter" :class="{ active: counter.toggleStart }" @dblclick="deleteCounter">
    <div class="time">
      <span> {{ timeFormatted }} </span>
    </div>
    <div class="line"></div>
    <div class="controls">
      <div class="button-wrapper" v-if="!counter.toggleStart">
        <button class="play" @click="start">
          <svg
            width="17"
            height="20"
            viewBox="0 0 17 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E" />
          </svg>
        </button>
      </div>
      <div class="button-wrapper" v-if="counter.toggleStart">
        <button class="pause" @click="pause">
          <svg
            width="10"
            height="20"
            viewBox="0 0 10 20"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <rect x="7" width="3" height="20" fill="white" />
            <rect width="3" height="20" fill="white" />
          </svg>
        </button>
      </div>
      <button class="stop" @click="stop">
        <svg
          width="20"
          height="20"
          viewBox="0 0 20 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect width="20" height="20" fill="#9E9E9E" />
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    counter: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      elapsedTime: 0,
      timer: 0,
      toggleStart: false
    }
  },
  computed: {
    timeFormatted() {
      var time = new Date(0, 0, 0, 0, 0, 0)
      time.setSeconds(this.elapsedTime / 1000)
      var seconds = time.getSeconds()
      var minutes = time.getMinutes()
      var hours = time.getHours()
      if (minutes === 0 && hours === 0) {
        return seconds
      } else {
        if (hours == 0) {
          return minutes + ':' + seconds
        } else {
          return hours + ':' + minutes + ':' + seconds
        }
      }
    }
  },
  methods: {
    toggleButton() {
      this.$emit('toggleStart', this.counter)
    },
    start() {
      this.timer = setInterval(() => {
        this.elapsedTime += 1000
      }, 100)
      this.toggleButton()
    },
    pause() {
      clearInterval(this.timer)
      this.toggleButton()
    },
    stop() {
      this.elapsedTime = 0
    },
    deleteCounter() {
      this.$emit('deleteCounter', this.counter)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/styles.scss';
.counter {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  @include rectangle();
}
.active {
  color: white;
  fill: white;
  .line {
    border-bottom: 1px solid white;
  }
  .stop {
    svg {
      rect {
        fill: white;
      }
    }
  }
}

.line {
  border-bottom: 1px solid $counter-color;
  width: 100%;
}
.time {
  @include center();
  width: 100%;
}
.controls {
  @include center();
  width: 100%;
  .button-wrapper {
    width: 20px;
    margin-right: 48px;
    button {
      width: 100%;
    }
  }
}
</style>
