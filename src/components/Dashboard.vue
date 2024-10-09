<template>
    <div id="burger-table">
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
        </div>
        <div id="burger-table-rows" v-for="burger in burgers" :key="burger.id">
            <div class="burger-table-row">
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div>{{ burger.carne }}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>

                    </ul>

                </div>
                <div>
                    <select name="status" class="status">
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">
                            {{ s.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deletarBurger(burger.id)">
                        Cancelar
                    </button>
                </div>
            </div>

        </div>
    </div>
</template>
<script>
export default {
    name: 'Dashboard',
    data() {
        return {
            burgers: null,
            burgersId: null,
            status: []
        }
    },
    methods: {
        async getPedidos() {

            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();

            this.burgers = data;
            this.getstatus();


        },
        async getstatus() {
            // status
            const req = await fetch("http://localhost:3000/status");
            const data = await req.json();

            this.status = data;
        },
        async deletarBurger(id) {

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE',
                headers: { "content-type": "application/json",
                    "Cache-Control": "no-cache"
                }});
            this.getPedidos();
        }
    },
    mounted() {
        this.getPedidos();
        this.getstatus();
        this.deletarBurger();
    }
}
</script>
<style scoped>
#burger-table {
    width: 950px;
    margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
    display: flex;
    flex-wrap: wrap;
}

#burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid black;
}

#burger-table-heading div,
.burger-table-row div {
    width: 19%;

}

.burger-table-row {
    width: 100%;
    padding: 12ṕx;
    border-bottom: 1px solid #aaa;
}

#burger-table-heading .order-id,
#burger-table-rows .order-number {
    width: 5%;
}

select {
    padding: 2px 2px;
    margin-right: 9px;
}

.delete-btn {
    background-color: #333;
    color: red;
    font-weight: bold;
    font-size: 16px;
    border: 1px solid black;
    border-radius: 20px;
    padding: 2px 5px;
    cursor: pointer;
    transition: .5s;
    margin: 0 auto;
}

.delete-btn:hover {
    color: #fcba03;
    background-color: transparent;
}
</style>