<template>
  <BannerVue />
  <div class="main-container">
      <h1>Monte seu burguer</h1>
      <p>formulario</p>
  </div>
</template>

<script>
  import BannerVue from '../components/Banner.vue';

  export default {
    name: 'Home',
    components: {
      BannerVue
    }
  }
</script>
