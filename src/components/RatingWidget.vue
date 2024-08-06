<template>
  <div class="rating-widget">
    <span v-for="star in stars" :key="star" @click="setRating(star)" class="star">
      {{ star <= rating ? '★' : '☆' }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    rating: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      stars: [1, 2, 3, 4, 5]
    }
  },
  methods: {
    setRating(star) {
      this.$emit('update:rating', star)
    }
  }
}
</script>

<style scoped>
.rating-widget {
  display: flex;
}

.star {
  font-size: 24px;
  cursor: pointer;
  color: #ddd;
}

.star:hover,
.star:hover ~ .star {
  color: #f39c12;
}
</style>
