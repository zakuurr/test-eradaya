<template>
  <div>
    <UploadImageVue />
    <ImageLibraryVue />
  </div>
</template>

<script>
import ImageLibraryVue from './components/ImageLibrary.vue';
import UploadImageVue from './components/UploadImage.vue';




export default {
  components: {
    UploadImageVue,
    ImageLibraryVue,
  },
};
</script>
