<template>
  <div>
    <h1>My Shop</h1>
    <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal"></navbar>
    <price-slider :sliderStatus="sliderStatus"></price-slider>
    <product-list :maximum="maximum" :products="products"></product-list>
  </div>
</template>

<script>
import ProductList from "./ProductList.vue";
import PriceSlider from "./PriceSlider.vue";
import Navbar from "./Navbar.vue";

export default {
  name: "Products",
  props: [
    "products",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
  ],
  components: {
    Navbar,
    ProductList,
    PriceSlider,
  },
};
</script>

<style scoped></style>
