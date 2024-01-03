<template>
  <div>
    <nav>
      <router-link to="/" id="logo-img">
        <img :src="Logos" :alt="descricao" id="logo">
      </router-link>
      <router-link to="/">Home</router-link> |
      <router-link to="/Pedidos">Pedidos</router-link>
    </nav>
</div>
</template>
<script>

export default{
    nome: 'Navbar',
    props:['Logos', 'descricao']
}
</script>

<style scoped>

nav{
  height: 10%;
  display: flex;
  padding: 15px;
  align-items: center;
  background: #222;
  justify-content: flex-end;
  border: 4px solid #111;
}

nav a{
  margin: 12px;
  transition: 0.5s;
  color: #FCBA03;
  text-decoration: none;
}

nav a:hover{
  color:white;
}

#logo{
  width: 50px;
  height: 50px;
}

#logo-img{
  margin: auto;
  margin-left: 0;
}

</style>