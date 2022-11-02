<template>
  <div>
    <header-vue />
    <promo-vue />
    <post-list />
    <footer-vue />
  </div>
</template>

<script>
import HeaderVue from "@/layout/Header.vue";
import PromoVue from "@/layout/Promo.vue";
import PostList from "@/layout/PostList.vue";
import FooterVue from "@/layout/Footer.vue";

export default {
  components: {
    'header-vue': HeaderVue,
    'promo-vue': PromoVue,
    'post-list': PostList,
    'footer-vue': FooterVue,
  }
}
</script>
<style lang="scss">
@import "./assets/scss/main.scss";
</style>
