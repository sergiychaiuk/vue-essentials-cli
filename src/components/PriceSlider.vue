<template>
  <transition
    name="custom"
    enter-active-class="animate__animated animate__fadeInDown"
    leave-active-class="animate__animated animate__slideOutRight"
  >
    <div v-if="sliderStatus">
      <div class="align-item-center" :class="sliderState">
        <label class="font-weight-bold mr-2" for="formMax">max</label>
        <input
          type="text"
          id="formMax"
          class="form-control mx-2 text-center"
          style="width: 60px"
          v-model="maxAmount"
          @change="$emit('update:maximum', maxAmount)"
        />
        <input
          type="range"
          class="custom-range w-100"
          min="0"
          max="200"
          v-model="maxAmount"
          @input="$emit('update:maximum', maxAmount)"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "PriceSlider",
  data: function () {
    return {
      maxAmount: 99,
    };
  },
  props: ["sliderStatus"],
  computed: {
    sliderState: function () {
      return this.sliderStatus ? "d-flex" : "d-none";
    },
  },
};
</script>

<style scoped></style>
