<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>

      <ul>
        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
      </ul>

      <div
        v-for="variant in variants"
        :key="variant.varientsId"
        class="color-box"
        :style="{ color: variant.variantColor }"
        @mouseover="updateProduct(variant.variantImage)"
      >
        <p>{{ variant.variantColor }}</p>
      </div>
    </div>

    <button
      v-on:click="addToCart"
      :disabled="!inStock"
      :class="{ disabledButton: !inStock }"
    >
      Add to Cart
    </button>

    <div class="cart">
      <p>Cart({{ cart }})</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: 'Socks',
      image: '',
      inStock: true,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: ''
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: ''
        }
      ],
      cart: 0
    }
  },
  methods: {
    addToCart() {
      this.cart += 1
    },
    updateProduct(variantImage) {
      this.image = variantImage
    }
  }
}
</script>

<style></style>
