<template>
  <div>
    <table class="table table-striped" style="width:80%; align:center" align="center">
      <thead>
        <tr>
          <th rowspan="2">No</th>
          <th>Category</th>
          <th>Title</th>
          <th>Description</th>
          <th>Price</th>
          <th>Stock</th>
          <th>Thumbnail</th>
        </tr>
        <tr>
          <td><input type="text" v-model="search.category" placeholder="Search"></td>
          <td><input type="text" v-model="search.title" placeholder="Search"></td>
          <td><input type="text" v-model="search.description" placeholder="Search"></td>
          <td><input type="text" v-model="search.price" placeholder="Search"></td>
          <td><input type="text" v-model="search.stock" placeholder="Search"></td>
          <td></td>
        </tr>
      </thead>
      <tbody>
        <product-row v-for="product in displayedProducts" :key="product.id" :product="product"></product-row>
      </tbody>
    </table>
    <div class="pagination">
      <button :disabled="currentPage === 1" @click="prevPage">Prev</button>
      <span>{{ currentPage }} of {{ totalPages }}</span>
      <button :disabled="currentPage >= totalPages" @click="nextPage">Next</button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted, watch } from 'vue';
import axios from 'axios';
import ProductRow from './ProductRow.vue';

const DATASET_URL = 'https://dummyjson.com/products';

const search = reactive({
  category: '',
  title: '',
  description: '',
  price: '',
  stock: '',
});
const currentPage = ref(1);
const totalPages = ref(1);
const products = ref([]);

const displayedProducts = ref([]);

const fetchData = async () => {
  try {
    const response = await axios.get(DATASET_URL, {
      params: {
        skip: (currentPage.value - 1) * 10,
        limit: 10,
        category: search.category,
        title: search.title,
        description: search.description,
        price: search.price,
        stock: search.stock,
      },
    });
    products.value = [...response.data.products];
    console.log(response.data.products)
    displayedProducts.value = products.value;
    totalPages.value = Math.ceil(response.data.total / 10);
  } catch (error) {
    alert(error.message);
  }
};

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
};

watch(currentPage, fetchData);

onMounted(fetchData);

</script>

<style scoped>
  
</style>