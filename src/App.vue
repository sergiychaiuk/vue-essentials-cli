<template>
  <div id="app" class="container mt-5">
    <router-view
      :cart="cart"
      :cartTotal="cartTotal"
      :products="products"
      :maximum.sync="maximum"
      :cartQty="cartQty"
      :sliderStatus="sliderStatus"
      @toggle="toggleSliderStatus"
      @delete="deleteItem"
      @add="addItem"
    ></router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data: function () {
    return {
      sliderStatus: false,
      maximum: 99,
      products: null,
      cart: [],
    };
  },
  computed: {
    cartTotal: function () {
      let sum = 0;
      this.cart.forEach(function (item) {
        sum = sum + item.product.price * item.qty;
      });
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      this.cart.forEach(function (item) {
        qty = qty + item.qty;
      });
      return qty;
    },
  },
  methods: {
    toggleSliderStatus: function () {
      this.sliderStatus = !this.sliderStatus;
    },
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
    deleteItem: function (id) {
      if (this.cart[id].qty > 1) {
        this.cart[id].qty--;
      } else {
        this.cart.splice(id, 1);
      }
    },
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
