<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <div class="table-responsive">
          <table class="table table-bordered">
            <tbody>
              <tr v-for="product in productList" :key="product.ProductID">
                <td>{{ product.ProductName }}</td>
                <td>{{ product.UnitPrice }}</td>
                <td>{{ product.Qty }}</td>
                <td>{{ product.TotalPrice }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';

const productList = ref([]);

onMounted(getProductList);

async function getProductList() {
  try {
    const response = await axios.get('https://crud.teamrabbil.com/api/v1/ReadProduct');
    if (response.status === 200) {
      productList.value = response.data.data;
    }
  } catch (error) {
    console.error('Error fetching product list:', error);
  }
}
</script>

<style>
/* Add your styling here */
</style>
