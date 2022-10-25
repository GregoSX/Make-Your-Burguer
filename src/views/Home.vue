<template>
  <BannerVue />
  <div class="main-container">
      <h1>Monte seu burguer</h1>
      <Form />
  </div>
</template>

<script>
  import Form from '@/components/Form.vue';
  import BannerVue from '../components/Banner.vue';

  export default {
    name: 'Home',
    components: {
      BannerVue,
      Form
    }
  }
</script>
