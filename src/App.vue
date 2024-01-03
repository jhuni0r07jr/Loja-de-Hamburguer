<template>
  <div>
    <Navbar :Logos="logo_img" :descricao="msg"/>
    <router-view/>
    <Footer/>

  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';


export default {
  components:{
    Navbar,
    Footer
  },
  data(){
    return{
      logo_img: './Img/logo.png',
      msg: 'Imagem de um sanduiche'
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family: Helvetica;
  box-sizing: border-box;
}

.corpo_do_site{
  width: 100%;
  height: 100%;
  min-height: 520px;
}

#imagem_ba{
  width: 100%;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: start;
  background-size: cover;
  background-position: center;
  background-image: url('../public/Img/burger.jpg');
}
</style>