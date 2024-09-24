<template>
    <p>componente de mensagem</p>
    <div>
        <form id="burger-form" @submit="createBurger">
            <div class="input-container">
                <label for="nome">Nome:</label>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
            </div>
            <div class="input-container">
                <label for="pao">Escolha o pão:</label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Escolha o pão:</option>
                    <option v-for="pao in paes" :key="pao.id" value="{{pao.tipo}}">{{pao.tipo}}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="carne">Carne:</label>
                <select name="carne" id="carne" v-model="carne">
                    <option value="">Escolha um corte:</option>
                    <option v-for="carne in carnes" :key="carne.id" value="{{ carne.tipo }}">{{ carne.tipo }}</option>
                </select>
            </div>
            <div class="input-container" id="opcionais-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcionais.id">
                    <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" value="{{opcional.tipo}}" />
                    <span>{{ opcional.tipo }}</span>
                </div>
                
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar meu Burger!">
            </div>
        </form>
    </div>
</template>
<script>
export default {
    name: 'Burgerform',
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            status: 'solicitando',
            msg: null
        }
    },
    methods: {
        async getIngredient() {
            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais

        },
        async createBurger(){
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitando"
            }
            const dataJson = JSON.stringify(data)
            console.log(dataJson)
        }
    },
    mounted(){
        this.getIngredient()
    }
}

</script>
<style scoped>
#burger-form {
    max-width: 30%;
    margin: 0 auto;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

.checkbox-container {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
    width: 50%;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
    background-color: #222;
    color: #fcba03;
    border: 4px solid #111;
    font-size: 16px;
    font-weight: bold;
    padding: 10px;
    border-radius: 20px;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover {
    background-color: #fcba03;
    color: #111
}

label {
    font-weight: bold;
    margin-bottom: 1px;
    padding: 5px 10px;
    color: #222;
    border-left: 4px solid #fcba03;
}

input,
select {
    padding: 5px 10px;
    width: 200px;
}

#opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais-title {
    width: 100%;
}
</style>