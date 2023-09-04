<template>
  <div class="container mt-4">
    <h2 class="text-3xl font-semibold mb-4">Galeri Gambar</h2>
 
    <div v-if="images.length === 0" class="text-gray-500">Belum ada gambar yang diunggah.</div>
    
    <div class="row">
    
      <div v-for="(image, index) in images" :key="index" class="col-lg-4 mb-4 mb-lg-0">
        <img :src="image" :alt="'Gambar ' + index"  class="w-100 shadow-1-strong rounded mb-4" @click="showImage(index)" />
  
    </div>
  </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
    };
  },
  mounted() {
  
    const storedImages = localStorage.getItem('uploadedImages');
    if (storedImages) {
      this.images = JSON.parse(storedImages);
    }
  },
  methods: {
    showImage(index) {
      console.log('Image clicked:', index);
    },
    addImage(imageUrl) {
      this.images.push({ url: imageUrl });
      localStorage.setItem('uploadedImages', JSON.stringify(this.images));
    },
  },
};
</script>
