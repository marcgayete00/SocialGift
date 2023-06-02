<script>
export default {
  data() {
    return {
      giftsData: [],
    };
  },
  props: {
    gift: {
      type: Object,
      required: true
    }
  },

  async mounted() {
    try {
      const response = await fetch(
        this.gift.product_url,
        {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json'
          }
        }
      );

      if (response.status === 200) {
        const data = await response.json();
        this.giftsData.push(data);
      } else {
        throw new Error(`Failed to fetch gift for url ${this.gift.product_url}.`);
      }
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<template>
  <div class="icon-container" v-for="giftData in giftsData" :key="giftData.id">
    <img :src="giftData.photo">
    <a>{{ giftData.name }}</a>
  </div>
</template>

<style scoped>
@import '../assets/Wishlists.css';
</style>