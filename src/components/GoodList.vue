<template>
  <div>
    <ul  class="itemContainer">
      <GoodItem
      v-for="good of goods"
      v-bind:good="good"
      v-on:put-to-basket="putToBasket"
      />
    </ul>
  </div>
</template>

<script>
  import GoodItem from '@/components/GoodItem';
  export default {
    props: ['goods'],
    components: {
      GoodItem
    },
    methods: {
      putToBasket(id) {
        this.$emit('put-to-basket', id)
      }
    }
  }
</script>

<style scoped src="@/css/style.css">
</style>