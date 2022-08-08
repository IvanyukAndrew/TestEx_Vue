<template lang="">
    <div class="cart-item">
        <img
            class="catalog-item-imges"
            v-bind:src="require('../assets/images/' + cart_item_data.image)"
            alt="img"
        >
        <div class="cart-item-info">
            <p>{{cart_item_data.name}}</p>
            <p>{{cart_item_data.price}}</p>
            <p>{{cart_item_data.article}}</p>
        </div>
    <button
        @click="deleteFromCart"
    >Delete</button>
    </div>
</template>
<script>
export default {
    name: 'cart-item-comp',
    props: {
        cart_item_data: {
            type: Object,
            default() {
                return {}
            }
        }
    },
    methods: {
        deleteFromCart() {
            this.$emit('deleteFromCart')
        }
    },
}
</script>
<style>
.cart-item {
    display: flex;
    flex-wrap: nowrap;
    justify-content: space-between;
    align-items: center;
    flex-basis: 25%;
    box-shadow: 0 0 8px 0 #e8e8e8;
    padding: 16px;
    margin-bottom: 40px;
}

.catalog-item-imges {
    max-width: 100px;
}
</style>