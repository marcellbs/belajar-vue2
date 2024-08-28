<template>
    <div>
        <h1 class="text-center text-info mt-5">IDShop</h1> 
        <NavBar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle-slide="toggleSlider" @delete-item="deleteItem"/>
        <PriceSlider :sliderStatus="sliderStatus" />
        <ProductList :maximum="maximum" :products="products" @add-item="addItem"></ProductList>
        <!-- :maximum.sync="maximum" -->
    </div>
</template>

<script>
import PriceSlider from './PriceSlider.vue';
import ProductList from './ProductList.vue';
import NavBar from './NavBar.vue';

export default {
    name : "AllProducts",
    props : [
        "products",
        "maximum",
        "cart",
        "cartQty",
        "cartTotal",
        "sliderStatus",
        "sliderState"
    ],

    components : {
        NavBar, PriceSlider, ProductList
    },

    methods : {
        toggleSlider: function() {
            this.$emit('toggle');
        },
        addItem : function(item) {
            this.$emit('add', item);
        },
        deleteItem : function(index) {
            this.$emit('delete', index);
        }
    }
}
</script>