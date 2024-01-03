<template>
  <div class="corpo_do_site">
    <PaginaPedidos/>
  </div>
</template>

<script>
import PaginaPedidos from '../components/PaginaPedidos.vue'
export default{
  nome: "Pedidos",

  components:{
    PaginaPedidos
  }
}
</script>
