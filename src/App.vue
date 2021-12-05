<template>
  <div id="app" class="container">
    <div class="header">
      <Nav class="headerNav"/>
      <Search
        @search="searchByTitle"
      />
    </div>
    <div class="goodsContainer">
      <div>
        <h1 class="galeryHeader">Картины эпохи возрождения</h1>
      </div>

      <GoodList
          v-bind:goods="goods"
          @put-to-basket="putToBasket"
      />
    </div>
    <div class="footerContainer">
      <Nav class="footerNav"/>
      <Phone/>
      <Location/>
    </div>
  </div>
</template>

<script>
import Nav from '@/components/Nav';
import GoodList from '@/components/GoodList';
import Search from '@/components/Search';
import Phone from '@/components/Phone';
import Location from '@/components/Location';
export default {
  name: 'App',
  data() {
    return {
      goods: [
        { id: 1, imgs: ['painting.png', 'img12'], title: 'Рождение Венеры', author: 'Сандро Боттичелли', price: '2 000 000', discountPrice: '1 000 000', inStock: true, inBusket: false, loading: false },
        { id: 2, imgs: ['ae973f6678e037cd297053384aa7dca0 1.png', 'img12'], title: 'Тайная Вечеря', author: 'Ленонардо да Винчи', price: '3 000 000', discountPrice: '', inStock: true, inBusket: false, loading: false},
        { id: 3, imgs: ['image-19 1.png', 'img12'], title: 'Сотворение Адама', author: 'Микеланджело', price: '6 000 000', discountPrice: '5 000 000', inStock: true, inBusket: false, loading: false},
        { id: 4, imgs: ['20152310142330 1.png', 'img12'], title: 'Урок Анатомии', author: 'Рембрандт', price: '', discountPrice: '', inStock: false, inBusket: false, loading: false }
      ]
    }
  },
  components: {
    Nav, GoodList, Search, Phone, Location//JSON.parse(localStorage.getItem("names"));
  },
  mounted() {
    if(localStorage.goods) this.goods = JSON.parse(localStorage.goods);
  },
  methods: {
    putToBasket(id) {
      this.goods = this.goods.map(good => {
        console.log(good)
        if (good.id === id) {
          good.loading = true;
          setTimeout(() => {
            good.loading = false;
            good.inBusket = !good.inBusket;
            localStorage.setItem("goods", JSON.stringify(this.goods));
            return good;
          }, 2000)
        }
        return good;
      })
    },
    searchByTitle(info) {
      this.goods = this.goods.filter((good) => good.title.toLowerCase().match(info.toLowerCase()))
    }
  }
}
</script>

<style src="@/css/style.css">
</style>
