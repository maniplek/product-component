<template>
  <div
    class="bg-cover min-h-[500px] w-1/2 p-5 relative"
    :style="{
      'background-color': mediaType === 'background' &&  backgroundColorDesktop,
      'background-size': 'cover',
      'background-size': 'cover',
      'background-position': 'center',
      'min-height': device === 'mobile' ? '500px' : '',
      'width': device === 'mobile' ? '80%' : '50%'
    }"
    ref="product"
  >
    <img
      v-if="mediaType === 'image'"
      :src="image"
      alt="picture"
      class="absolute top-0 left-0 bottom-0 right-0 object-fill"
    />
    <div
      class="all-details absolute"
      :style="{
        color: textColor,
        top: device === 'desktop' ? '0' : 'auto',
        bottom: device === 'mobile' ? '0' : 'auto',
        left: '0',
        right: '0',
        padding:'10px',
        top: textPositionD.includes('top') ? '0' : 'auto',
        bottom: textPositionD.includes('bottom') ? '0' : 'auto',
        left: textPositionM.includes('left') ? '0' : 'auto',
        right: textPositionM.includes('right') ? '0' : 'auto',
      }"
    >
      <p class="font-medium text-sm leading-1rem">{{displayName}}</p>
      <div class="description font-normal">
        <span class="font-normal text-sm leading-1rem">{{ product.priceOriginal }}</span>
        <span class="font-normal text-xs leading-1rem px-2 line-through">{{ product.price }}</span>
        <span class="font-normal text-xs leading-1rem px-2">-{{ product.discount }}</span>
      </div>
      <div class="availability">
        <p class="font-normal text-xs leading-4" v-if="product.isAvailable == true">AVAILABLE</p>
        <p class="font-normal text-xs leading-4" v-if="product.isAvailable == false">AVAILABLE SOON</p>
      </div>
      <p class="font-normal text-xs leading-4" >{{ product.colors }} COLORS</p>
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
    mediaType: String,
    textPositionD: String,
    textPositionM: String,
  },
  data() {
    return {
      device: "desktop",
    };
  },
  computed: {
    displayName() {
    return this.device === 'mobile' ? 'Lorem ipsum dolor sit amet' : this.product.name;
  },

    image() {
      let width = window.innerWidth;
      if (!this.picture) return "default-background.jpg";
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
      switch (this.device) {
        case "mobile":
          return this.textPositionM || "";
        case "desktop":
          return this.textPositionD || "";
      }
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


