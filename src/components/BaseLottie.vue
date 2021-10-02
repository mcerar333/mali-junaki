<template>
  <div class="lottie-container" ref="lottie"></div>
</template>

<script>
import lottie from 'lottie-web';

export default {
  name: 'BaseLottie',

  props: {
    options: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      anim: null,
      animName: this.getUniqueName(),
    };
  },
  mounted() {
    this.anim = lottie.loadAnimation({
      renderer: 'svg',
      container: this.$refs.lottie,
      loop: this.options.loop ?? true,
      autoplay: this.options.autoplay ?? true,
      animationData: this.options.animationData,
      rendererSettings: this.options.rendererSettings,
    });
  },
  beforeUnmount() {
    lottie.destroy(this.animName);
  },
  methods: {
    getUniqueName() {
      return (
        Date.now().toString(36) +
        Math.random()
          .toString(36)
          .slice(2)
      );
    },
  },
};
</script>

<style lang="scss">
.lottie-container {
  width: 100%;
  height: 100%;
  overflow: hidden;
}
</style>
