<template>

  <div class="container-fluid container-xl px-2 px-xl-5">
    <div class="px-0 px-xl-5">
      <BannerHome/>
      <NavSearch/>
      <CardsProduct/>
    </div>
  </div>
  
</template>

<script>
import BannerHome from '@/components/BannerHome/BannerHome'
import NavSearch from '@/components/NavSearch/NavSearch'
import CardsProduct from '@/components/CardsProduct/CardsProduct'

export default {
  name: 'Home',
  components:{BannerHome,NavSearch,CardsProduct},
}
</script>

<style src="./style.scss" lang="scss" scoped />