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
          <td class="py-2 px-4 border">{{ product.name }}</td>
          <td class="py-2 px-4 border">{{ product.stock }}</td>
          <td class="py-2 px-4 border">${{ product.price }}</td>
          <td class="py-2 px-4 border">{{ product.expiryDate }}</td>
          <td class="py-2 px-4 border">{{ product.creationDate }}</td>
          <td class="py-2 px-4 border">{{ product.supplier }}</td>
          <td class="py-2 px-4 border flex gap-2">
            <button @click="$emit('edit-product', product)" class="bg-blue-500 text-white px-2 py-1 rounded">Editar</button>
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
  }
  </script>
  