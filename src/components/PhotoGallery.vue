<template>
  <div class="photo-gallery">
    <div v-for="image in images" :key="image.title" class="photo-card">
      <Tooltip :text="image.title">
        <img :src="image.image_url" :alt="image.title" />
      </Tooltip>
      <div class="photo-info">
        <h3>{{ image.title }}</h3>
        <RatingWidget :rating="image.rating" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Tooltip from './Tooltip.vue'
import RatingWidget from './RatingWidget.vue'

export default {
  components: {
    Tooltip,
    RatingWidget
  },
  data() {
    return {
      images: []
    }
  },
  async created() {
    try {
      const response = await axios.get(`${import.meta.env.VITE_API_URL}`)
      this.images = response.data.images || []
    } catch (error) {
      console.error('Error fetching images:', error)
    }
  }
}
</script>

<style scoped>
.photo-gallery {
  display: flex;
  flex-wrap: wrap;
}

.photo-card {
  position: relative;
  border: 1px solid #ddd;
  border-radius: 8px;
  margin: 10px;
  overflow: hidden;
  width: 27%;
}

.photo-card img {
  width: 100%;
  height: auto;
}

.photo-info {
  padding: 10px;
}
</style>
