<template>
<center>

        <input type="text" v-model="searchQuery" placeholder="Search"
</center>
<template v-if="searchQuery">
      <div class="row pr-5 pl-5 d-flex justify-content-center">
    <div class="p-5 col-5" v-for="product in products">
      <div class="card">
        <img :src="product.image_url" alt="Product Image" style="width: 100%" />
        <div class="container">
            <h4>
              <b>{{ product.title }}</b>
            </h4>
            <p>£{{ product.price.min }}</p>
            <button type="button" class="btn btn-primary">View</button>
        </div>
      </div>
    </div>
  </div>
    </template>
</template>

<script setup>
import { ref, watch } from 'vue';

const searchQuery = ref('');
var products = [];

watch(searchQuery, (newQuery) => {
  fetch("https://aix.salesfire.co.uk/api/searcha?client_id=dbf1dbc9-a940-48c2-b44b-0bb6dc63924e&query="+newQuery+"&limit=12&page=1")
    .then(response => response.json())
    .then(data => (products = data.products));
});

</script>