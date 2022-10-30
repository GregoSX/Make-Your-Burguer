<template>
    <div id="burguer-table">
        <div>
            <div id="burguer-table-heading">
                <div class="order-id">#:</div>
                <div>Client</div>
                <div>Bread</div>
                <div>Meat</div>
                <div>Optional</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="burguer-table-rows">
            <div class="burguer-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{burger.id}}</div>
                <div>{{burger.name}}</div>
                <div>{{burger.bread}}</div>
                <div>{{burger.meat}}</div>
                <div>
                    <ul>
                        <li v-for="(optional, index) in burger.options" :key="index">{{optional}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status">
                        <option value="">Status</option>
                        <option v-for="s in status" :key="s.id" value="s.tipo" :selected="burger.status == s.tipo">{{s.tipo}}</option>
                    </select>
                    <button class="delete-btn">Cancel</button>
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
                burgers_id: null,
                status: []
            }
        },
        methods: {
            async getPedidos() {
                const req = await fetch ("http://localhost:3000/burgers")

                const data = await req.json()

                this.burgers = data

                this.getStatus() 
            },
            async getStatus() {
                const req = await fetch ("http://localhost:3000/status")

                const data = await req.json()

                this.status = data
            }
        },
        mounted() {
            this.getPedidos() 
        }
    }
</script>

<style scoped>
    #burguer-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #burguer-table-heading, #burguer-table-rows, .burguer-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #burguer-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #burguer-table-heading div, .burguer-table-row div {
        width: 19%;
    }

    .burguer-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #burguer-table-heading .order-id, .burguer-table-row .order-number{
        width: 5%;
    }

    select {
        padding: 10px 6px;
        margin-right: 12px;
    }

    .delete-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 8px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover {
        background-color: #444;
        border: 2px solid #444;
        color: #fdc52a;
    }

</style>