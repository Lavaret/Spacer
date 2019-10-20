<style lang="scss" scoped>

.hero-image {
  z-index: -1;
  position: fixed;
  top: 0;
  width: 100%;
  height: 100vh;
  min-height: 100vh;
  background-image: url('../assets/heroimage.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 80% 0%;
}

.hero-image::after {
  content: '';
  background: rgba(0, 0, 0, .45);
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 100vh;
}

</style>

<template>

<div class="hero-image">
</div>

</template>

<script>

export default {
  name: 'HeroImage',
};

</script>
