<template>
    <nav class="navbar navbar-light bg-light fixed-top">
          <div class="navbar-text ms-auto d-flex me-3">
            <button class="btn btn-sm btn-outline-success" @click="$emit('toggle-slide')">
              <FontAwesomeIcon icon="dollar-sign"/>
            </button>
            <div class="dropdown ml-2" v-if="cart.length > 0">
              <button id="dropdownCart" data-bs-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="btn btn-success btn-sm dropdown-toggle">
                <!-- <b>Cart:</b> -->
                <span class="badge rounded-pill text-bg-success">{{ cartQty }}</span>
                <FontAwesomeIcon icon="shopping-cart" />
                <!-- {{ cartTotal | currencyFormat }} -->
                <PriceItem :value="Number(cartTotal)"></PriceItem>
                
              </button>
              <div class="dropdown-menu dropdown-menu-end" aria-labelledby="dropdownCart">
                <div class="btn-group" v-for="(item, index) in cart" :key="index">
                  <div class="dropdown-item text-end">
                    <span class="badge rounded-pill text-bg-warning align-text-top mr-1">
                      {{ item.qty }}
                    </span>
                    {{ item.product.name }}
                    <b>{{ item.product.price * item.qty | currencyFormat }} </b>
                    <a href="#" class="badge text-bg-danger link-underline link-underline-opacity-0" @click.stop="$emit('delete-item', index)">&#x2715;</a>
                  </div>
                </div>

                <router-link class="btn btn-sm btn-outline-info text-dark float-right mr-2" to="/checkout">Checkout</router-link>

              </div>
            </div>
          </div>
      </nav>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import PriceItem from './PriceItem.vue';
export default {
    name : "NavBar",
    components: { 
        PriceItem,
        FontAwesomeIcon
    },
    props : ['cart', 'cartQty', 'cartTotal'],
    filters: {
        currencyFormat : function (val) {
            return 'Rp' + Number.parseFloat(val).toFixed(2);
        } 
    }, 
}
</script>