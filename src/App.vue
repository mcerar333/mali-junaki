<template>
  <BaseCard v-for="card in cards" :key="card.id" :card-info="card" />
</template>

<script>
import BaseCard from '@/components/BaseCard.vue';

export default {
  name: 'App',
  components: { BaseCard },

  data() {
    return {
      cards: [],
    };
  },
  async created() {
    const cards = await this.getJson('/server/response.json');

    cards.forEach(async card => {
      const lottie = await this.getJson(card.lottie);

      this.cards.push({
        id: card.id,
        title: card.title,
        description: card.description,
        image: card.image,
        animationData: lottie,
      });
    });
  },
  methods: {
    async getJson(url) {
      const res = await fetch(url);

      if (!res.ok) throw Error('Unable to fetch.');
      const data = await res.json();

      return data;
    },
  },
};
</script>
