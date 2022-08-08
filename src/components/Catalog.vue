<template>
    <div class="catalog">
        <div class="catalog__link_to_card">Корзина: {{ CART.length }}</div>
        <h1>Catalog</h1>
        <Selecte
            :options="categories"
            @select="sortByOption"
            :selected="selected"
        />
        <div class="catalog__list">
            <CatalogItem v-for="product in filteredProducts" :key="product.article" :productData="product"
                @addToCart="addToCart" />
        </div>
    </div>
</template>
<script>
import CatalogItem from '@/components/CatalogItem.vue'
import { mapActions, mapGetters } from 'vuex'
import Selecte from './Selecte.vue'

export default {
    name: 'v-catalog',

    components: {
        CatalogItem,
        Selecte
    },

    data() {
        return {
            categories: [
                { name: 'Всі', value: 'all' },
                { name: 'Хлопці', value: 'male' },
                { name: 'Дівчата', value: 'femal' },
            ],
            selected: 'Всі',
            sortedProducts: []
        }
    },
    computed: {
        ...mapGetters([
            'PRODUCTS',
            'CART'
        ]),
        filteredProducts() {
            if (this.sortedProducts.length) {
                return this.sortedProducts
            } else {
                return this.PRODUCTS
            }
        }
    },
    methods: {
        ...mapActions([
            'GET_PRODUCTS_FROM_API',
            'ADD_TO_CART'
        ]),
        addToCart(data) {
            this.ADD_TO_CART(data)
        },

        sortByOption(option) {
            this.sortedProducts = []
            this.PRODUCTS.map(item => {
                if(item.categories === option.name) {
                    this.sortedProducts.push(item)
                    console.log(this.sortedProducts)
                }
            })
        },

        optionSelect(option) {
            this.selected = option.name
        }
    },
    mounted() {
        this.GET_PRODUCTS_FROM_API()
    },
}
</script>
<style>
.catalog__list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
}

.catalog__link_to_card {
    position: absolute;
    top: 10px;
    right: 10px;
    padding: 16px;
    border: solid 1px #aeaeae;
    position: fixed;
}
</style>