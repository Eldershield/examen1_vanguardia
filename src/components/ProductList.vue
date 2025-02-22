<template>
    <table class="min-w-full bg-white border border-gray-300">
      <thead>
        <tr class="bg-gray-200">
          <th class="py-2 px-4 border">Código</th>
          <th class="py-2 px-4 border">Nombre</th>
          <th class="py-2 px-4 border">Stock</th>
          <th class="py-2 px-4 border">Precio</th>
          <th class="py-2 px-4 border">Fecha de Vencimiento</th>
          <th class="py-2 px-4 border">Fecha de Creación</th>
          <th class="py-2 px-4 border">Proveedor</th>
          <th class="py-2 px-4 border">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id" class="border-t">
          <td class="py-2 px-4 border">{{ product.id }}</td>
          <td class="py-2 px-4 border">
            <input v-if="editingProduct?.id === product.id" v-model="editingProduct.name" class="border px-2 py-1 w-full" />
            <span v-else>{{ product.name }}</span>
          </td>
          <td class="py-2 px-4 border">
            <input v-if="editingProduct?.id === product.id" v-model="editingProduct.stock" type="number" class="border px-2 py-1 w-full" />
            <span v-else>{{ product.stock }}</span>
          </td>
          <td class="py-2 px-4 border">
            <input v-if="editingProduct?.id === product.id" v-model="editingProduct.price" type="number" class="border px-2 py-1 w-full" />
            <span v-else>${{ product.price }}</span>
          </td>
          <td class="py-2 px-4 border">
            <input v-if="editingProduct?.id === product.id" v-model="editingProduct.expiryDate" type="date" class="border px-2 py-1 w-full" />
            <span v-else>{{ product.expiryDate }}</span>
          </td>
          <td class="py-2 px-4 border">{{ product.creationDate }}</td>
          <td class="py-2 px-4 border">
            <input v-if="editingProduct?.id === product.id" v-model="editingProduct.supplier" class="border px-2 py-1 w-full" />
            <span v-else>{{ product.supplier }}</span>
          </td>
          <td class="py-2 px-4 border flex gap-2">
            <button v-if="editingProduct?.id === product.id" @click="saveEdit" class="bg-green-500 text-white px-2 py-1 rounded">Guardar</button>
            <button v-else @click="startEditing(product)" class="bg-blue-500 text-white px-2 py-1 rounded">Editar</button>
            <button @click="$emit('delete-product', product.id)" class="bg-red-500 text-white px-2 py-1 rounded">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script>
  export default {
    props: {
      products: Array,
    },
    data() {
      return {
        editingProduct: null,
      };
    },
    methods: {
      startEditing(product) {
        this.editingProduct = { ...product };
      },
      saveEdit() {
        this.$emit('update-product', this.editingProduct);
        this.editingProduct = null;
        alert('rpodcuto actulizado correctamente!');
      },
    },
  };
  </script>
  
  