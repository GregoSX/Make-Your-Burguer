<template>
  <div class="main-container">
    <h1>Manage orders</h1>
    <Dashboard id="dash"/>
  </div>
</template>

<script>
  import Dashboard from '@/components/Dashboard.vue'
  
  export default {
    name: 'Pedidos',
    components: { 
      Dashboard 
    },
  }
</script>

<style scoped>
  .main-container {
    margin-bottom: 190px;
  }
</style>