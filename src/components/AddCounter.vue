<template>
  <div class="add">
    <button @click="createCounter">
      <svg
        width="20"
        height="20"
        viewBox="0 0 20 20"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect x="8.5" width="3" height="20" fill="#9E9E9E" />
        <rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)" fill="#9E9E9E" />
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  methods: {
    createCounter() {
      this.$emit('create')
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/styles.scss';
.add {
  @include center();
  @include rectangle();
}
</style>
