<template>
    <div class="container mt-5">
      <h1 class="text-center">Lista de Productos</h1>
      <div class="row">
        <div
          v-for="producto in productos"
          :key="producto.id"
          class="col-md-4"
        >
          <div class="card mb-4 shadow-sm zoom-card">
            <img :src="producto.image" class="card-img-top" alt="producto imagen" />
            <div class="card-body">
              <h5 class="card-title">{{ producto.title }}</h5>
              <p class="card-text">{{ producto.description }}</p>
              <p><strong>Precio: </strong> ${{ producto.price }}</p>
              <p><strong>Categoría: </strong> {{ producto.category }}</p>
              <p>
                <strong>Rating: </strong> {{ producto.rating.rate }}
                ({{ producto.rating.count }} reviews)
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const productos = ref([]);
  
  const fetchProductos = async () => {
    try {
      const response = await fetch('https://fakestoreapi.com/products');
      const data = await response.json();
      productos.value = data;
    } catch (error) {
      console.error('Error al obtener los productos:', error);
    }
  };
  
  onMounted(() => {
    fetchProductos();
  });
  </script>
  
  <style scoped>
  .card-img-top {
    height: 200px;
    object-fit: cover;
  }
  
  .zoom-card {
    transition: transform 0.3s ease, background-color 0.3s ease;
  }
  
  .zoom-card:hover {
    transform: scale(1.1);
    background-color: #e0f7fa; /* Un azul claro */
  }
  </style>
  