<template>
  <div>
    <Product
      :product="product"
      :picture="picture"
      :backgroundColorDesktop="backgroundColorDesktop"
      :backgroundColorTablet="backgroundColorTablet" 
      :backgroundColorMobile="backgroundColorMobile" 
      :textColor="textColor"
    />
  </div>
</template>
<script>
import Product from "./components/Product.vue";
import data from "./data/index";

export default {
  name: "App",
  components: {
    Product,
  },
  data() {
    return {
      product: data.product,
      picture: data.picture,
      backgroundColorDesktop: data.backgroundColorDesktop,
      backgroundColorTablet: data.backgroundColorTablet,
      backgroundColorMobile: data.backgroundColorMobile,
      textColor: data.textColor
    };
  },
};
</script>