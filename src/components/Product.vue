<template>
  <div
    class="h-screen w-full bg-cover p-5 relative"
    :style="{
      'background-color': backgroundColor,
      'background-size': 'cover',
      'background-position': 'center',
    }"
    ref="product"
  >
    <img
      :src="image"
      alt=" picture"
      class="absolute top-0 left-0 bottom-0 right-0 object-fill "
    />
    <div
      class="all-details absolute"
      :style="{
        color: textColor,
        top: device === 'desktop' ? '0' : 'auto',
        bottom: device === 'mobile' ? '0' : 'auto',
        left: '0',
        right: '0',
        padding: '20px',
        
      }"
    >
      <p class="font-medium leading-5">{{ product.name }}</p>
      <div class="description font-normal">
        <span class="">{{ product.priceOriginal }}</span>
        <span class="px-2 line-through">{{ product.price }}</span>
        <span class="px-2">-{{ product.discount }}</span>
      </div>
      <div class="availability font-normal">
        <p v-if="product.isAvailable == true">AVAILABLE</p>
        <p v-if="product.isAvailable == false">AVAILABLE SOON</p>
      </div>
      <p>{{ product.colors }} COLORS</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: Object,
    picture: Object,
    backgroundColorDesktop: String,
    backgroundColorTablet: String,
    backgroundColorMobile: String,
    textColor: String,
  },
  data() {
    return {
      device: "desktop",
    };
  },
  computed: {
    image() {
      let width = window.innerWidth;
      if (width <= 500) {
        this.device = "mobile";
        return `${this.picture.imageMobile}`;
      } else if (width <= 1024) {
        this.device = "tablet";
        return `${this.picture.imageTablet}`;
      } else {
        this.device = "desktop";
        return `${this.picture.imageDesktop}`;
      }
    },
    backgroundColor() {
      let width = window.innerWidth;
      if (width <= 500) {
        return this.backgroundColorMobile;
      } else if (width <= 1024) {
        return this.backgroundColorTablet;
      } else {
        return this.backgroundColorDesktop;
      }
    },
    textPosition() {
      return this.device === "mobile" ? "bottom-left" : "top-left";
    },
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    handleResize() {
      this.device = window.innerWidth <= 500 ? "mobile" : "desktop";
    },
  },
};
</script>
