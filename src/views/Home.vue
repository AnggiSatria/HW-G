<template>
  <div class="containers">
    <h1 class="subtxt">Welcome to HWG App</h1>
    <Autocomplete v-if="images.length > 0" :images="images" />
    <ImageCarousel />
    <RatingWidget :rating="rating" @update:rating="rating = $event" />
  </div>
</template>

<script>
import Autocomplete from '../components/Autocomplete.vue'
import ImageCarousel from '../components/ImageCarousel.vue'
import Tooltip from '../components/Tooltip.vue'
import RatingWidget from '../components/RatingWidget.vue'
import axios from 'axios'

export default {
  components: {
    Autocomplete,
    ImageCarousel,
    Tooltip,
    RatingWidget
  },
  data() {
    return {
      images: [], // Initialize as an empty array
      rating: 3
    }
  },
  async created() {
    try {
      const response = await axios.get(`${import.meta.env.VITE_API_URL}`)
      this.images = response.data.images || [] // Ensure images is an array
    } catch (error) {
      console.error('Error fetching images:', error)
    }
  }
}
</script>

<style scoped>
.containers {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 20px;
}

.subtxt {
  width: 100%;
  margin: auto;
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 40px;
}
</style>
