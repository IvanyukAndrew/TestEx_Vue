<template>
    <div class="cart">
        Корзина
        <CartItem 
            v-for="(item, index) in cart_data"
            :key="item.article"
            :cart_item_data="item"
            @deleteFromCart="deleteFromCart(index)"
        />
        <div class="cart__total">
            <p class="total__name">Total:</p>
            <p>{{cartTotalCost}} grn</p>
        </div>
    </div>
</template>

<script>
import CartItem from './CartItem.vue'
import { mapActions } from 'vuex'
    export default {
        name: "v-cart",
        components: {
            CartItem
        },
        props: {
            cart_data: {
                type: Array,
                default() {
                    return []
                }
            }
        },
        methods: {
            ...mapActions([
                'DELETE_FROM_CART'
            ]),
            deleteFromCart(index) {
                this.DELETE_FROM_CART(index)
            }
        },
        computed: {
            cartTotalCost() {
                let result = []

                for(let item of this.cart_data) {
                    result.push(item.price)
                }

                result = result.reduce(function (sum, el) {
                    return sum + el
                })
                return result
            }
        }
}
</script>

<style>
.cart {
    margin-bottom: 100px;
}
.cart__total {
    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;
    padding: 14px;
    display: flex;
    justify-content: center;
    background: #26ae68;
    color: #fff;
    font-size: 20px;
}
.total__name {
    margin-right: 8px;
}
</style>