<template>
  <div ref="lavContainer" class="door-animation"></div>
</template>

<script>
import lottie from 'lottie-web'
export default {
  props: {
    options: {
      type: Object,
      required: true,
    },
    width: {
      type: Number,
      required: true,
      defaults: 400,
    },
    start: {
      type: Boolean,
      defaults: false,
    },
  },

  watch: {
    start(val, old) {
      if (val === true) {
        this.anim.play()
      }
    },
  },

  mounted() {
    this.anim = lottie.loadAnimation({
      container: this.$refs.lavContainer,
      renderer: 'svg',
      loop: false,
      autoplay: false,
      animationData: this.options.animationData.default,
      rendererSettings: this.options.rendererSettings,
    })
    this.$emit('animCreated', this.anim)
    this.anim.addEventListener('complete', () => {
      this.$emit('complete', true)
    })
  },
}
</script>
<style lang="scss" scoped>
.door-animation {
  width: 100%;
  overflow: hidden;
}
@media (max-width: 576px) {
  .door-animation {
    width: 100%;
  }
}
</style>
