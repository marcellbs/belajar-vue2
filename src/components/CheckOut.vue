<template>
    <div>
        <h1>Checkout</h1>
        <table class="table table-hover" v-if="cart.length">
            <caption class="text-end h3">
                <b>Total : </b>
                <PriceItem class="d-block text-success fw-light" 
                :value="Number(cartTotal)">
                </PriceItem>
            </caption>
            <thead>
                <tr>
                    <th scope="col"></th>
                    <th scope="col">Item</th>
                    <th scope="col" class="text-center">Qty</th>
                    <th scope="col" class="text-end">Price</th>
                    <th scope="col" class="text-end">Sub Total</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, index) in cart" :key="item.product.id">
                    <td class="text-center">
                        <div class="btn-group">
                            <div @click="$emit('add', item.product)" class="btn btn-info">+</div>
                            <div @click="$emit('delete', index
                            )" class="btn btn-outline-info">-</div>
                        </div>
                    </td>
                    <th scope="row">{{ item.product.name }}</th>
                    <th class="text-center">{{ item.qty }}</th>
                    <th class="text-end">{{ Number(item.product.price) }}</th>
                    <th class="text-end">
                        {{ Number(item.product.price * item.qty) }}
                    </th>

                </tr>
            </tbody>
        </table>
        <router-link class="btn btn-sm btn-outline-info text-dark" to="/">Back to Shop</router-link>
    </div>
</template>

<script>
    import PriceItem from './PriceItem.vue';
    export default {
        name : "CheckOut",
        props : ["cart", "cartTotal"],
        components : {
            PriceItem
        }
    }
</script>