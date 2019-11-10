<template>
    <div class="heroImage" />
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style scoped>
  .heroImage {
    position: fixed;
    width: 100%;
    height: 100vh;
    top: 0;
    z-index: -1;
    background-image: url("../assets/header_image.jpeg");
    background-repeat: no-repeat;
    background-size: cover;
  }
</style>
