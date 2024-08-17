<template>
  <div class="carousel">
    <button @click="prev">Previous</button>
    <div class="carousel-slide" v-if="images.length">
      <img :src="images[currentIndex].image_url" :alt="images[currentIndex].title" />
    </div>
    <button @click="next">Next</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      images: [],
      currentIndex: 0
    }
  },
  async created() {
    try {
      const response = await axios.get(`${import.meta.env.VITE_API_URL}`)
      this.images = response.data.images || []
    } catch (error) {
      console.error('Error fetching images:', error)
    }
  },
  methods: {
    next() {
      if (this.images.length) {
        this.currentIndex = (this.currentIndex + 1) % this.images.length
      }
    },
    prev() {
      if (this.images.length) {
        this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length
      }
    }
  }
}

console.log()
</script>

<style scoped>
.carousel {
  display: flex;
  align-items: center;
}

.carousel-slide {
  flex: 1;
  text-align: center;
}

.carousel-slide img {
  max-width: 100%;
  height: auto;
}

button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px;
  cursor: pointer;
}
</style>
