<template>
<!--  <img :src="preloader" alt="loader">-->
  <h2>loading ...</h2>
</template>

<script>
import preloader from '@/assets/Spinner-1.2s-231px.svg'

export default {
  name: 'pre-loader',
  data() {
    return {
      preloader
    }
  }
}
</script>

<style scoped>

</style>