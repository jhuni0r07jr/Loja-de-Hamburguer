<template>
    <mensagem :msg="msg" v-show="msg"/>
    <div id="main">
        <form id="burger-form" @submit.prevent="createBurguer">
            <div class="inputs">
                <label for="nome">Nome:</label><br>
                <input type="text" id="nome" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="inputs">
                <label for="pao">Escolha o Pão</label><br>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Selecione o seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :v-model="pao.tipo">{{pao.tipo}}</option>
                </select>
            </div>
            <div class="inputs">
                <label for="carne">Escolha a sua carne</label><br>
                <select name="carne" id="carne" v-model="carne">
                    <option value="">Selecione o seu Hamburguer</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                </select>
            </div>
            <div class="inputs">
                <label for="Queijo">Escolha o queijo</label><br>
                <select name="Queijo" id="Queijo" v-model="Queijo">
                    <option value="">Selecione o queijo</option>
                    <option v-for="Queijo in Queijos" :key="Queijo.id" :value="Queijo.tipo">{{Queijo.tipo}}</option>
                </select>
            </div>
            <input type="submit" id="Enviar" value="Enviar">

        </form>
    </div>
</template>

<script>
    import Mensagem from "./Mensagem.vue";
export default{
    nome: 'FormularioBurger',
    data(){
        return{
            pao: null,
            nome: null,
            carne: null,
            Queijo: null,
            paes: null,
            carnes: null,
            Queijos: null,
            msg: null
        }
    },
    methods:{
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.Queijos = data.Queijos;
        },
            async createBurguer(){
            const data = {
                carne: this.carne,
                pao: this.pao,
                nome: this.nome,
                Queijo: this.Queijo,
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/burgers",{
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });
            const res = await req.json();

            this.msg = `Pedido do(a): `+ res.nome+ ` criado com sucesso`
            setTimeout(() => this.msg ="", 3000);
            this.pao = "";
            this.nome = "";
            this.carne = "";
            this.Queijo = "";
        }
    },
    mounted(){
        this.getIngredientes();
},
    components:{
        Mensagem
    }
}
</script>

<style scoped>
    #main{
        width: 50%;
        margin: auto;
        height: 100%;
        display: flex;
        margin-top: 20px;
        font-weight: 550;
        font-size: larger;
        margin-bottom: 90px;
        align-items: center;
        justify-content: center;
    }

    #main h2{
        align-items: center;
        text-align: center;
    }

    .inputs{
        width: 100%;
        margin-top: 10px;
    }

    input{
        border: 1px solid black;
    }

    .inputs select, input{
        width: 100%;
        height: 25px;
        margin: auto;
        font-size: 20px;
        text-align: center;
        align-items: center;
        border-radius: 20px;
    }

    .inputs label{
        margin: auto;
        padding-left: 10px;
        text-align: center;
        align-items: center;
        border-left: 5px solid orange;
    }

    #Enviar{
        cursor: pointer;
        transition: .5s;
        margin-top: 20px;
        font-weight: 600;
        color: #fcba23;
        background: #222;
    }

    #Enviar:hover{
        color: #222;
        border: #fcba23;
        background: #fcba23;
    }
</style>