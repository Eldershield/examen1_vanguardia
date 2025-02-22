<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Control de Inventario de Bodega</h1>
    <product-form @add-product="addProduct" />
    <product-list
      :products="products"
      @edit-product="editProduct"
      @delete-product="deleteProduct"
    />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import ProductForm from './components/ProductForm.vue'
import ProductList from './components/ProductList.vue'

export default {
  components: {
    ProductForm,
    ProductList,
  },
  setup() {
    const products = ref([])

    onMounted(() => {
      const storedProducts = localStorage.getItem('products')
      if (storedProducts) {
        products.value = JSON.parse(storedProducts)
      }
    })

    const saveProducts = () => {
      localStorage.setItem('products', JSON.stringify(products.value))
    }

    const addProduct = (product) => {
      products.value.push(product)
      saveProducts()
      alert('Producto almacenado correctamente')
    }

    const editProduct = (updatedProduct) => {
      const index = products.value.findIndex(
        (product) => product.id === updatedProduct.id
      )
      if (index !== -1) {
        products.value[index] = updatedProduct
        saveProducts()
        alert('Producto actualizado correctamente')
      }
    }

    const deleteProduct = (productId) => {
      if (confirm('¿Está seguro de eliminar el producto?')) {
        products.value = products.value.filter(
          (product) => product.id !== productId
        )
        saveProducts()
      }
    }

    return {
      products,
      addProduct,
      editProduct,
      deleteProduct,
    }
  },
}
</script>
