<!-- eslint-disable vue/no-use-v-if-with-v-for -->
<template>
    <transition-group name="fade" tag="div" enter-active-class="animate__animated animate__fadeInLeft" leave-active-class="animate__animated animate__fadeOutRight">
        <div class="row mb-3 align-items-center" v-for="(item, index) in showItem" :key="item.id" :data-index="index">
          <div class="col-1 m-auto">
              <button class="btn btn-info" @click="$emit('add-item', item)">+</button>
              
          </div>
          <div class="col-sm-4">
              <img :src="item.image" :alt="item.name" class="img-fluid d-block">
          </div>
          <div class="col">
              <h3 class="text-info">{{ item.name }}</h3>
              <p class="mb-0">{{ item.description }}</p>
              <div class="h5 fw-bold text-end">
                <PriceItem :value="Number(item.price)"></PriceItem>
              </div>
          </div>
        </div>
      </transition-group>
</template>

<script>
import PriceItem from './PriceItem.vue';

    export default {
        name: "product-list",
        components: {
            PriceItem
        },
        props: ["products", 'maximum'],
        computed : {
            showItem: function(){
                let max = this.maximum;
                return this.products.filter(function (item){
                    return Math.trunc(item.price) <= max;
                });
            }
        },
        methods : {
            // before: function(el){
            //   el.className = 'd-none'
            // },
            // enter: function(el){
            //   let delay = el.dataset.index * 100;
            //   setTimeout(function() {
            //     el.className = 'row d-flex mb-3 align-items-center animate__animated animate__fadeInRight'
            //   }, delay)
            // },
            // leave: function(el){
            //   let delay = el.dataset.index * 100;
            //   setTimeout(function() {
            //     el.className = 'row d-flex mb-3 align-items-center animate__animated animate__fadeOutRight'
            //   }, delay)
            // },
        },
    }
</script>