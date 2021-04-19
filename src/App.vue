<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <p class="animate__animated animate__fadeInRight">
      Take a look at our offerings below
    </p>
    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "App",
  components: {
    FontAwesomeIcon,
  },
};
</script>
