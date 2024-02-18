<template>
    <div>

        <Mensagem :msg="msg" v-show="msg" />
        <form id="carro-form" @submit="createCarro">

            <div class="input-container">
                <label for="nome">Proprietário:</label>
                <input type="text" id="nome" v-model="nome" placeholder="Informe o Nome:">
            </div>
            <div class="input-container">
                <label for="veiculo">Modelo do Veiculo:</label>
                <input type="text" id="veiculo" v-model="veiculo" placeholder="Informe o Modelo:">
            </div>
            <div class="input-container">
                <label for="placa">Placa do veículo</label>
                <input type="text" id="placa" v-model="placa" placeholder="Informe a Placa:">
            </div>

            <div class="input-container">
                <label for="hora">Horário de entrada:</label>
                <input type="text" id="hora" v-model="hora" placeholder="Informe o Horário de Entrada:">
            </div>

            <div class="input-container">
                <input type="submit" class="submit-btn" value="Cadastrar Veículo">
            </div>

        </form>
    </div>
</template>


<script>

import Mensagem from './Mensagem.vue';

export default {
    name: "CarroForm",

    data() {
        return {
            nome: null,
            veiculo: null,
            placa: null,
            hora: null,
            msg: null,

        }
    },
    methods: {
        async createCarro(e) {
            e.preventDefault();

            const data = {
                nome: this.nome,
                veiculo: this.veiculo,
                placa: this.placa,
                hora: this.hora,
                status: "Solicitado",

            }
            // console.log(data)
            const dataJson = JSON.stringify(data);

            // Fazendo o POST

            const req = await fetch("http://localhost:3000/carros", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            console.log(res)

            //Mensagem de sucesso
            this.msg = `${this.veiculo} de ${this.nome} cadastrado com sucesso`;

            // Limpar a mensagem
            setTimeout(() => this.msg = "", 3000);

            // Limpar formulário

            this.nome = "";
            this.veiculo = "";
            this.placa = "";
            this.hora = "";
        }
    },
    components: {
        Mensagem,
    }
}



</script>




<style scoped>
#carro-form {
    max-width: 300px;
    margin: 0 auto;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 5px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #3F7FBF;
}

input {
    padding: 6px 10px;
    widows: 300px;
}

input:focus {
    border-radius: 8px;
}

.submit-btn {
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

.submit-btn:hover {
    background-color: #003468;
}
</style>