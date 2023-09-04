<template>
    <div class="container mt-4">
      <h2>Upload Image</h2>
      <div class="mb-3">
        <label for="imageUpload" class="form-label">Pilih Gambar</label>
        <input type="file" class="form-control" id="imageUpload" accept="image/*" @change="uploadImage" />
      </div>
      <div v-if="message" class="alert alert-info">{{ message }}</div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        message: null,
      };
    },
    methods: {
  async uploadImage(event) {
    const selectedFile = event.target.files[0];

    if (!selectedFile) return;

    const allowedExtensions = /\.(jpg|jpeg|bmp|png|gif)$/i;

    if (!allowedExtensions.test(selectedFile.name)) {
      this.message = 'Hanya boleh file gambar.';
      return;
    }

    if (selectedFile.size > 2 * 1024 * 1024) {
      this.message = 'File gambar terlalu besar.';
      return;
    }

    const formData = new FormData();
    formData.append('image', selectedFile);

    try {
      const response = await this.$axios.post(
        `https://api.imgbb.com/1/upload?key=${process.env.VUE_APP_IMGBB_API_KEY}`,
        formData
      );

      if (response.data.status === 200) {
        const imageUrl = response.data.data.url;
        const storedImages = JSON.parse(localStorage.getItem('uploadedImages')) || [];
        storedImages.push(imageUrl);
        localStorage.setItem('uploadedImages', JSON.stringify(storedImages));
        this.message = 'Gambar berhasil diupload.';
        this.$emit('refresh-images');
      } else {
        this.message = 'Upload error.';
      }
    } catch (error) {
      console.error(error);
      this.message = 'Upload error.';
    }
  },
},

  };
  </script>
  
  <style scoped>
  /* Tambahkan styling sesuai kebutuhan Anda */
  </style>
  