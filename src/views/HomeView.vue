<template>
  <div class="corpo_do_site">
    <Banner/>
    <h2>Home</h2>
    <FormularioBurger/>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import FormularioBurger from '../components/FormularioBurger.vue'
export default {
components:{
  Banner,
  FormularioBurger
}
}
</script>
<style scoped>

  h2{
    text-align: center;
    align-items: center;
  }

</style>