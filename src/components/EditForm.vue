<template>
  <div class="form-container">
    <div class="form-box">
      <form @submit.prevent="editProduct">
        <h1>Add New Product</h1>
        <div class="form-group">
            <label for="product-name">Product Name</label>
            <input type="text" class="form-control" id="product-name" v-model="productName" placeholder="Product Name">
        </div>
        <div class="form-group">
          <label for="product-image">Product Image Url</label>
          <input type="text" class="form-control" id="product-image" v-model="productUrl" placeholder="Product Image Url">
        </div>
        <div class="form-row">
          <div class="form-group col-md-3">
            <label for="product-price">Price</label>
            <input type="text" class="form-control" id="product-price" v-model="productPrice" placeholder="Product Price">
          </div>
          <div class="form-group col-md-6">
            <label for="product-category">Category</label>
            <select id="product-category" class="form-control">
              <option selected>Choose...</option>
              <option>...</option>
            </select>
          </div>
          <div class="form-group col-md-3">
            <label for="product-stock">Stock</label>
            <input type="number" class="form-control" id="product-stock" v-model="productStock" placeholder="Stock">
          </div>
        </div>
        <button type="submit" class="btn btn-primary btn-block"><span class="fas fa-pen-square"></span> Edit Product</button>
      </form>
    </div>
  </div>
</template>

<script>
import Swal from 'sweetalert2'

export default {
  name: 'EditForm',
  data () {
    return {
      productId: '',
      productName: '',
      productUrl: '',
      productPrice: '',
      productStock: ''
    }
  },
  methods: {
    setDefaultValue () {
      const product = this.$store.state.product
      this.productId = product.id
      this.productName = product.name
      this.productUrl = product.image_url
      this.productPrice = product.price
      this.productStock = product.stock
    },
    editProduct () {
      const product = {
        id: this.productId,
        name: this.productName,
        imageUrl: this.productUrl,
        price: this.productPrice,
        stock: this.productStock
      }
      this.$store.commit('set_product', product)
      this.$store.dispatch('editProduct')
        .then(({ data }) => {
          Swal.fire({
            icon: 'success',
            title: 'Success Update Product Data',
            text: `${product.name} data is updated`
          })
          this.productId = ''
          this.productName = ''
          this.productUrl = ''
          this.productPrice = ''
          this.productStock = ''
          this.$router.push({ name: 'product' })
        })
        .catch(err => {
          console.log(err.response)
          Swal.fire({
            icon: 'error',
            title: 'Something Went Wrong',
            text: `${err.response}`
          })
        })
    }
  },
  created () {
    this.setDefaultValue()
  }

}
</script>

<style scoped>
.form-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
}

.form-box {
    padding: 10px;
    width: 65%;
    background-color: rgb(233, 230, 230);
    border-radius: 10px;
    -webkit-box-shadow: -1px 10px 13px -1px rgba(0,0,0,0.75);
    -moz-box-shadow: -1px 10px 13px -1px rgba(0,0,0,0.75);
    box-shadow: -1px 10px 13px -1px rgba(0,0,0,0.75);
    font-family: 'Bree Serif', serif;
    font-size: larger;
    margin: 10px;
}
</style>