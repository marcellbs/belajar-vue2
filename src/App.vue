<template>
  <div id="app" class="container mt-5">
    <router-view 
    :cart="cart"
    :cartQty="cartQty"
    :cartTotal="cartTotal"
    :maximum.sync="maximum"
    :products="products"
    :sliderStatus="sliderStatus"
    @toggle="toggleSliderStatus"
    @add="addItem"
    @delete="deleteItem"
    ></router-view>
  </div>
</template>

<script>
// import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';


export default {
  name: 'App',
  data : function() {
    return {
      maximum : 25,
      products : [],
      cart : [],
      sliderStatus : false,

    }
  },
  

  mounted: function () {
      fetch('https://hplussport.com/api/products/order/price')
      .then(res => res.json())
      .then(data => {
        this.products = data;
      })
  },

  methods : {
    addItem: function(product){
          let productIndex;
          let productExist = this.cart.filter(function(item, index){
            if(item.product.id == Number(product.id)){
              productIndex = index;
              return true;
            } else {
              return false;
            }
          });

          if(productExist.length) {
            this.cart[productIndex].qty++;
          } else {
            this.cart.push({
              product : product, 
              qty : 1
            })
          }
    },

    deleteItem : function(key) {
        if(this.cart[key].qty > 1 ) {
          this.cart[key].qty--;
        } else {
          this.cart.splice(key, 1);
        }
    },

    toggleSliderStatus : function(){
      this.sliderStatus = !this.sliderStatus ;
    }
  },

  computed : {
    
      cartTotal : function() {
        let sum = 0;
        for(let key in this.cart ){
          sum += (this.cart[key].product.price * this.cart[key].qty);
        }

        return sum;
      },
      
      cartQty : function() {
        let qty = 0;
        for(let key in this.cart ){
          qty += this.cart[key].qty;
        }

        return qty;
      },
  }
}
</script>
