<template>
  <Navbar :logo="logoData" :alt="altData"/>
  <router-view/>
  <Footer />
</template>

<script>
  import Footer from './components/Footer.vue';
  import Navbar from './components/Navbar.vue';

  export default {
    components: {
      Navbar,
      Footer
    },
    data() {
      return {
        logoData: "/img/logo.png",
        altData: "Logo do sistema"
      }
    }
  }
</script>

<style>
  * {
    font-family: Helvetica;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  .main-container {
    margin: 48px;
    min-height: 250px;
  }

  h1 {
    color: #222;
    font-size: 40px;
    margin-bottom: 32px;
    text-align: center;
  }

</style>
