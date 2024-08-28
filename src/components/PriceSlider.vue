<template>
    <transition name="custom" enter-active-class="animate__animated animate__fadeInDown" leave-active-class="animate__animated animate__slideOutRight">
        <div v-if="sliderStatus">
          <div class="align-items-center" :class="sliderState">
            <label for="" class="fw-bold mr-2">Max</label>
            <input type="number" name="number" id="number" class="form-control mx-2" v-model="maxAmount" @change="$parent.$emit('update:maximum', maxAmount)">
            <br>
            <input type="range" name="custom-range" id="custom-range" class="custom-range" min="0" max="200" v-model="maxAmount" @input="$parent.$emit('update:maximum', maxAmount)">
          </div>
        </div>
      </transition>
</template>

<script>
export default {
    name : "PriceSlider",
    data : function(){
        return {
            maxAmount: 24,
        }
    },
    props : ["sliderStatus", "maximum"],
    computed : {
        sliderState : function() {
            return this.sliderStatus ? 'd-flex' : 'd-none';
        },
    }
}
</script>

<style scoped>
    .fade-enter, .fade-leave-to {
        opacity: 0;
    }

    .fade-enter-active, .fade-leave-active {
        transition: all 1s ease-in-out;
    }
</style>