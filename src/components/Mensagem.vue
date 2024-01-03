<template>
    <div>
        <p>{{msg}}</p>
    </div>
</template>
<script>

export default{
 nome: "Mensagem",

 props:{
    msg: String
 }
}

</script>

<style scoped>
    p{
    width: 40%;
    height: 40px;
    margin: auto;
    display: flex;
    margin-top: 20px;
    text-align: center;
    border-radius: 10px;
    align-items: center;
    justify-content: center;
    background: #30b7ec;
    }
</style>