<template>
    <div class="catalog-item">
        <img
            class="catalog-item-img"
            v-bind:src="require('../assets/images/' + productData.image)"
            alt="img"
        >
        <p class="catalog-item-name">{{productData.name}}</p>
        <p class="catalog-item-price">price: {{productData.price}} grn</p>
        <button
            class="catalog-item-add-to-cart-btn btn"
            @click="addToCart"
        >add to cart</button>
    </div>
</template>
<script>
export default {
    name: 'catalog-item',
    props: {
        productData: {
            type: Object,
            default() {
                return {}
            }
        }
    },
    methods: {
        addToCart() {
            this.$emit('addToCart', this.productData)
        }
    },
}
</script>
<style>
.catalog-item {
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e8e8e8;
    padding: 16px;
    margin-bottom: 16px;
}

.catalog-item-img {
    width: 200px;
}
</style>