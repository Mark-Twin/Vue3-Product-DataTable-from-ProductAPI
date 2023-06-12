<template>
  <tr>
    <td>{{ product.id }}</td>
    <td>{{ product.category }}</td>
    <td>{{ product.title }}</td>
    <td>{{ product.description }}</td>
    <td>{{ product.price }}</td>
    <td>{{ product.stock }}</td>
    <td> <img :src="props.product.thumbnail" alt="thumbnail" width="100" height="100"></td>>
  </tr>
</template>
<!-- <script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
};

</script> -->
<script setup>
import {defineProps} from 'vue'
const props = defineProps({
  product: {
    type: Object,
    required: true
  }
})
</script>
