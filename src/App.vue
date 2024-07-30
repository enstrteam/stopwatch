<script>
import Counter from './components/Counter.vue'
import AddCounter from './components/AddCounter.vue'
export default {
  components: {
    Counter,
    AddCounter
  },
  data() {
    return {
      counters: [
        {
          id: 1,
          elapsedTime: 0,
          timer: 0,
          toggleStart: false
        },
        {
          id: 2,
          elapsedTime: 0,
          timer: 0,
          toggleStart: false
        }
      ]
    }
  },
  methods: {
    createCounter() {
      var lastCounterID = 0
      if (this.counters.length) {
        lastCounterID = [...this.counters].pop().id
      }
      const newCounter = {
        id: lastCounterID + 1,
        elapsedTime: 0,
        timer: 0,
        toggleStart: false
      }
      this.counters.push(newCounter)
    },
    toggleStart(counter) {
      counter.toggleStart = !counter.toggleStart
    },
    deleteCounter(counter) {
      this.counters = this.counters.filter((el) => el.id !== counter.id)
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <div class="counters" v-for="counter in counters" :key="counter.id">
      <Counter
        :counter="counter"
        :key="counter.id"
        @toggleStart="toggleStart"
        @deleteCounter="deleteCounter"
      />
    </div>
    <AddCounter @create="createCounter" />
  </div>
</template>

<style lang="scss">
@import './assets/styles.scss';

body {
  background-color: $main-background;
  height: 100vh;
  @include center();
}

.wrapper {
  display: grid;
  gap: 50px;
  @media screen and (min-width: 768px) {
    grid-template-columns: repeat(2, 1fr);
  }
  @media screen and (min-width: 1024px) {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
