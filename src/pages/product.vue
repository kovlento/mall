<template>
  <div class="product">
    <product-param>
      <template v-slot:buy>
        <button class="btn">立即购买</button>
      </template>
    </product-param>
    <div class="h">123</div>
  </div>
</template>

<script>
import ProductParam from './../components/ProductParams'
export default {
  components: { ProductParam }
}
</script>

<style lang="scss">
.product {
  .h {
    height: 1000px;
  }
  .btn {
    margin-left: 10px;
  }
}
</style>
