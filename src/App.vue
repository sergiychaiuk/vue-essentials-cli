<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <price-slider
      :sliderStatus="sliderStatus"
      :maximum.sync="maximum"
    ></price-slider>
    <product-list
      :maximum="maximum"
      :products="products"
      @add="addItem"
    ></product-list>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import PriceSlider from "./components/PriceSlider.vue";

export default {
  name: "App",
  data: function () {
    return {
      sliderStatus: true,
      maximum: 99,
      products: null,
      cart: [],
    };
  },
  methods: {
    addItem: function (product) {
      let whichProduct;
      let existing = this.cart.filter(function (item, index) {
        if (Number(item.product.id) === Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });

      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
  },
  components: {
    ProductList,
    PriceSlider,
  },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
};
</script>
