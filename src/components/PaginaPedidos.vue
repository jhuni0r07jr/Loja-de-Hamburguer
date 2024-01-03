<template>
    <div id="Tabela">
        <table>
            <tr id="Cabecalho">
                <td>Id do pedido</td>                
                <td>Cliente</td>
                <td>Pão</td>
                <td>Carne</td>
                <td>Queijo</td>
                <td id="Situacao">Situação</td>
            </tr>
            <tr class="corpo_tabela" v-for="burguer in burgers" :key="burguer.id" :v-model="burguer.tipo">
                <td>{{burguer.id}}</td>
                <td>{{burguer.nome}}</td>
                <td>{{burguer.carne}}</td>
                <td>{{burguer.pao}}</td>
                <td>{{burguer.Queijo}}</td>

                <td>
                    <select name="status" id="status" @change="Atualizacao($event, burguer.id)">
                        <option value="">Selecione</option>
                        <option v-for="status in status" :key="status.id" :value="status.tipo" :selected="burguer.status == status.tipo">{{status.tipo}}</option>
                    </select>

                    <button class="deletar" @click="DeletarBurguer(burguer.id)">Deletar</button>
                </td>
            </tr>
        </table>
    </div>
</template>
<script>

export default{
    nome: "PaginaPedidos",
    data(){
        return{
            burgers: null,
            burguer_id: null,
            status: []
        }
    },
    methods:{
        async Pedidos(){
        const req = await fetch("http://localhost:3000/burgers");
        const data = await req.json();

        this.burgers = data;
        this.getstatus();
    },

    async getstatus(){
        const req = await fetch("http://localhost:3000/status");
        const data = await req.json();
        
        this.status = data;
    },
    async DeletarBurguer(id){
        const req = await fetch(`http://localhost:3000/burgers/${id}`,{
        method: 'DELETE',
        });

        const retorno = await req.json();

        this.Pedidos()        
    },

    async Atualizacao (event, id){
        const opcao = event.target.value;
        const json = JSON.stringify({status: opcao})

        const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: 'PATCH',
            headers: {"Content-Type": "application/json"},
            body: json
        })

    }
},
    mounted(){
        this.Pedidos(this.burgers)
    }
}
</script>

<style scoped>
#Tabela{
    width: 100%;
    margin: auto;
    display: flex;
    min-width: 120px;
    overflow-y: auto;
    align-items: center;
    justify-content: center;
}

table{
    width: 50%;
    height: 100%;
    margin-top: 100px;
    border-collapse: collapse;
}

#Cabecalho{
    width: 100%;
    font-weight: 700;
    text-align: center;
    align-items: center;
}

#Cabecalho td{
    background: #dbd9d9;
    border: 1px solid black;
    border-bottom: 3px solid #333;
}
.corpo_tabela td{
    border: 1px solid black;
    padding: 8px;
    text-align: center;
    align-items: center;
}

select{
    width: 110px;
    height: 40px;
    margin-left: 2px;
    text-align: center;
    align-items: center;
}
.deletar{
    width: 60px;
    height: 40px;
    border: none;
    cursor: pointer;
    font-weight: 700;
    color: #e2c523;
    background: #333;
}

</style>