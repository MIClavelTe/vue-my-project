<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" />
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>
      <p>Shipping: {{ shipping }}</p>

      <ul>
        <li v-for="(detail, index) in details" :key="index">{{ detail }}</li>
      </ul>

      <div
        v-for="(variant, index) in variants"
        :key="variant.varientsId"
        class="color-box"
        :style="{ color: variant.variantColor }"
        @mouseover="updateProduct(index)"
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

    <ProductTabs :reviews="reviews" />
  </div>
</template>

<script>
import ProductTabs from './productTabs'
import eventBus from '../eventBus'
export default {
  components: {
    ProductTabs
  },
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      brand: 'Vue Mastery',
      product: 'Socks',
      selectedVariant: 0,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: '',
          variantQuantity: 10
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: '',
          variantQuantity: 0
        }
      ],
      reviews: []
    }
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
    },
    updateProduct(index) {
      this.selectedVariant = index
      // console.log(index)
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product
    },
    image() {
      return this.variants[this.selectedVariant].variantImage
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity
    },
    shipping() {
      if (this.premium) {
        return 'Free'
      }
      return 2.99
    }
  },
  mounted() {
    eventBus.$on('review-submitted', productReview => {
      this.reviews.push(productReview)
    })
  }
}
</script>

<style></style>
