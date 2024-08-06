<template>
  <div class="autocomplete">
    <input v-model="query" @input="filterItems" placeholder="Search..." />
    <div class="photo-gallery">
      <div v-for="image in filteredImages" :key="image.title" class="photo-card">
        <img :src="image.image_url" :alt="image.title" />
        <div class="photo-info">
          <h3>{{ image.title }}</h3>
          <RatingWidget :rating="image.rating" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import RatingWidget from './RatingWidget.vue'

export default {
  components: {
    RatingWidget
  },
  props: {
    images: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      query: '',
      filteredImages: this.images
    }
  },
  methods: {
    filterItems() {
      this.filteredImages = this.images.filter((image) =>
        image.title.toLowerCase().includes(this.query.toLowerCase())
      )
    }
  }
}
</script>

<style scoped>
.autocomplete {
  position: relative;
}

input {
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}

.photo-gallery {
  display: flex;
  flex-wrap: wrap;
}

.photo-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  margin: 10px;
  overflow: hidden;
  width: 22.5%;
}

.photo-card img {
  width: 100%;
  height: auto;
}

.photo-info {
  padding: 10px;
}
</style>
