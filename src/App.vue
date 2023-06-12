<template>
  <div id="app">
    <ProductList />
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue'
import 'bootstrap/dist/css/bootstrap.css'
export default {
  name: 'App',
  components: {
    ProductList
  }
}
</script>

