<template>
  <div class="main-wrapper">
    <Catalog />
    <Cart
      v-if="CART.length"
      :cart_data="CART"
    />
  </div>
</template>

<script>
import Catalog from '@/components/Catalog.vue'
import Cart from '@/components/Cart.vue'
import { mapGetters } from 'vuex'

export default {
  name: 'main-wrapper',
  components: {
    //   //   Header
    Catalog,
    Cart,
},
  computed: {
    ...mapGetters([
      'CART'
    ])
  },
}
</script>

<style>
.main-wrapper {
  max-width: 900px;
  margin: 0 auto;
}
</style>