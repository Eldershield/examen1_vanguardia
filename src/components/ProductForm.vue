<template>
  <form @submit.prevent="handleSubmit" class="mb-4">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
      <div>
        <label class="block">Nombre del Producto</label>
        <input v-model="product.name" type="text" class="w-full p-2 border" />
      </div>
      <div>
        <label class="block">Stock</label>
        <input v-model="product.stock" type="number" class="w-full p-2 border" />
      </div>
      <div>
        <label class="block">Precio</label>
        <input v-model="product.price" type="number" step="0.01" class="w-full p-2 border" />
      </div>
      <div>
        <label class="block">Fecha de Vencimiento</label>
        <input v-model="product.expiryDate" type="date" class="w-full p-2 border" />
      </div>
      <div>
        <label class="block">Proveedor</label>
        <input v-model="product.supplier" type="text" class="w-full p-2 border" />
      </div>
    </div>
    <button type="submit" class="mt-4 px-4 py-2 bg-blue-500 text-white">
      Agregar Producto
    </button>
  </form>
</template>

<script>
import { ref } from 'vue';
import { v4 as uuidv4 } from '@lukeed/uuid';

export default {
  props: {
    productToEdit: Object,
  },
  setup(props, { emit }) {
    const product = ref({
      id: '',
      name: '',
      stock: '',
      price: '',
      expiryDate: '',
      creationDate: '',
      supplier: '',
    });

    const handleSubmit = () => {
      
      if (
        !product.value.name ||
        !product.value.stock ||
        !product.value.price ||
        !product.value.expiryDate ||
        !product.value.supplier
      ) {
        alert('Todos los campos son obligatorios');
        return;
      }

      
      product.value.id = uuidv4();
      product.value.creationDate = new Date().toISOString().split('T')[0];

      
      emit('add-product', { ...product.value });
      
      
      
      resetForm();
    };

    const resetForm = () => {
      product.value = {
        id: '',
        name: '',
        stock: '',
        price: '',
        expiryDate: '',
        creationDate: '',
        supplier: '',
      };
    };

    return {
      product,
      handleSubmit,
    };
  },
};
</script>
