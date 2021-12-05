<template>
  <li>
    <div :id="good.id" class="itemDescribe" v-bind:class="{sold: !good.inStock}">
      <div>
        <div>
          <img v-bind:src="require('@/img/' + good.imgs[0])" v-bind:class="{opacity: !good.inStock}" />
        </div>
        <div v-bind:class="{opacity: !good.inStock, descrideText: !good.inStock}">
          {{good.title}}
        </div>
        <div v-bind:class="{opacity: !good.inStock, descrideText: !good.inStock}">
          {{good.author}}
        </div>
      </div>

      <div v-bind:class="{itemBuy: good.inStock }" v-if="good.inStock">
        <div class="itemPrice">
          <p v-bind:class="{ priceTextDiscount: good.discountPrice, priceText: !good.discountPrice }">
            {{good.price}}
          </p>
          <p class="priceText">
            {{good.discountPrice}}
          </p>
        </div>
        <button v-on:click="$emit('put-to-basket', good.id)" class="buyButton" ><Loader v-if="good.loading"/>
          <div class="buttonText">
            {{good.inBusket ? 'В корзине' : 'Купить'}}
          </div>
        </button>
      </div>

      <div v-else class="soldText">
        Продан на аукционе
      </div>

    </div>
  </li>
</template>

<script>
import Loader from '@/components/Loader';
  export default {
    props: {
      good: {
        type: Object,
        required: true
      }
    },
    components: {
      Loader
    }
  }
</script>

<style scoped src="@/css/style.css">
</style>
