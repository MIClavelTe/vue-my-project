<template>
  <div>
    <Product :premium="premium" />
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
      premium: true
    }
  }
}
</script>

<style></style>
