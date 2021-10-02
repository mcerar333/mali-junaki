<template>
  <div class="card">
    <figure class="card__asset" :class="{ playing: isPlaying }">
      <transition name="fade" mode="out-in">
        <BaseLottie v-if="isPlaying" :options="lottieOptions" />
        <img
          v-else
          :src="cardInfo.image"
          :alt="`mali junak ${cardInfo.id}`"
          class="card__image"
        />
      </transition>
    </figure>

    <div class="card__content">
      <h3>{{ cardInfo.title }}</h3>
      <p>{{ cardInfo.description }}</p>
    </div>

    <button class="btn btn--more" @click="isPlaying = !isPlaying">
      <span>{{ buttonText }}</span>
    </button>
  </div>
</template>

<script>
import BaseLottie from '@/components/BaseLottie.vue';

export default {
  name: 'BaseCard',
  components: { BaseLottie },

  props: {
    cardInfo: {
      type: Object,
      required: true,
    },
  },

  data() {
    return {
      isPlaying: false,
    };
  },
  computed: {
    lottieOptions() {
      return { animationData: this.cardInfo.animationData };
    },
    buttonText() {
      return this.isPlaying ? 'Stop Video' : 'Play Video';
    },
  },
};
</script>

<style lang="scss">
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
</style>
