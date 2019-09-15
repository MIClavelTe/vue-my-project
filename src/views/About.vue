<template>
  <div>
    <div class="cart">
      <p>Cart({{ cart.length }})</p>
    </div>

    <Product :premium="premium" @add-to-cart="updateCart" />
  </div>
</template>

<script>
import Product from './product'
export default {
  components: {
    Product
  },
  data() {
    return {
      premium: true,
      cart: []
    }
  },
  methods: {
    updateCart(id) {
      this.cart.push(id)
    }
  }
}
</script>

<style></style>
