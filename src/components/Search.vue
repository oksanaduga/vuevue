<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" placeholder="Поиск по названию картины" class="input">
    <button type="submit" class="search">
       Найти
    </button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: '',
    }
  },
  methods: {
    onSubmit() {
      console.log('Submit', this.title)
      const titleForSearch = this.title.trim();
      if (titleForSearch) {
        this.$emit('search', titleForSearch)
        this.title = ''
      }
    }
  }
}
</script>

<style scoped src="@/css/style.css">
</style>