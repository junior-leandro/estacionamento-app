<template>
    <div id="carro-table">

        <Mensagem :msg="msg" v-show="msg" />


        <div>
            <div id="carro-table-heading">
                <div class="order-id">ID:</div>
                <div>Proprietário </div>
                <div>Modelo do Veiculo: </div>
                <div>Placa do Veiculo: </div>
                <div>Horario de Entrada: </div>
                <div>Ações: </div>

            </div>

        </div>
        <div id="carro-table-rows">

            <div class="carro-table-row" v-for="carro in carros" :key="carro.id">

                <div class="order-number"> {{ carro.id }}</div>
                <div> {{ carro.nome }} </div>
                <div> {{ carro.veiculo }} </div>
                <div> {{ carro.placa }} </div>
                <div> {{ carro.hora }} </div>
                <div>

                    <select name="status" class="status" @change="updateCarro($event, carro.id)">
                        <option :value="s.tipo" v-for="s in status" :key="s.tipo" :selected="carro.status == s.tipo">{{
                            s.tipo }} </option>
                    </select>

                    <button class="delete-btn" @click="deletarVeiculo(carro.id)">Deletar</button>


                </div>

            </div>

        </div>
    </div>
</template>

<script>

import Mensagem from './Mensagem.vue';

export default {
    name: "Dashboard",

    data() {
        return {
            carros: null,
            carros_id: null,
            status: [],
            msg: null,

        }
    },
    // Carregar os veiculos

    components: {
        Mensagem

    },

    methods: {
        async getCadastros() {

            const req = await fetch("http://localhost:3000/carros");
            const data = await req.json();

            this.carros = data;

            this.getStatus();
        },

        async getStatus() {

            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();

            this.status = data;


        },


        async deletarVeiculo(id) {
            const req = await fetch(`http://localhost:3000/carros/${id}`, {

                method: "DELETE"
            });

            const data = await req.json();

            //Mensagem de sucesso
            this.msg = `Veiculo deletado com sucesso`;

            // Limpar a mensagem
            setTimeout(() => this.msg = "", 3000);
            this.getCadastros();

        },

        async updateCarro(event, id) {
            const opcoes = event.target.value;
            const dataJson = JSON.stringify({ status: opcoes });

            const req = await fetch(`http://localhost:3000/carros/${id}`, {

                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            //Mensagem de sucesso
            this.msg = `Veiculo alterado para ${res.status} sucesso!`;

            // Limpar a mensagem
            setTimeout(() => this.msg = "", 3000);


        }

    },
    mounted() {
        this.getCadastros();
    }
}
</script>

<style scoped>
#carro-table {
    max-width: 1280px;
    margin: 0 auto;

}

#carro-table-heading,
#carro-table-rows,
.carro-table-row {
    display: flex;
    flex-wrap: wrap;

}

#carro-table-heading {
    font-weight: 700;
    padding: 12px;
    border-bottom: 3px solid rgba(53, 30, 180);
}

#carro-table-heading div,
.carro-table-row div {
    width: 19%;
}


.carro-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid rgba(53, 30, 180);
}

#carro-table-heading .order-id,
   .carro-table-row .order-number {
       width: 5%;
   }


select {
    padding: 10px 6px;
    margin-right: 12px;
}

.delete-btn {
    background-color: #3F7FBF;
    color: #ffffff;
    font-weight: bold;
    padding: 10px;
    font-size: 16px;
    border: 2px solid white;
    cursor: pointer;
    transition: .5s;
    border-radius: 8px;
}

.delete-btn:hover {
    background-color: #003468;
}
</style>