<template>
    <div v-if="!haverOrdes">
        <p id="message">There are no orders registered</p>
    </div>
    <div id="burguer-table" v-else>
        <Message :msg="msg" v-show="msg"/>
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
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                        <option value="">Status</option>
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">{{s.tipo}}</option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancel</button>
                </div>
            </div>
        </div>
    </div>
</template>


<script> 
    import Message from './Message.vue'

    export default {
        name: 'Dashboard',
        data() {
            return {
                burgers: null,
                burgers_id: null,
                status: [],
                msg: null,
                haverOrdes: false
            }
        },
        components: {
            Message
        },
        methods: {
            async getPedidos() {
                const req = await fetch ("http://localhost:3000/burgers")

                const data = await req.json()

                if(data.length === 0) {
                    this.haverOrdes = false
                }
                else {
                    this.haverOrdes = true
                    this.burgers = data
                    this.getStatus() 
                }
                
            },
            async getStatus() {
                const req = await fetch ("http://localhost:3000/status")

                const data = await req.json()

                this.status = data
            },
            async deleteBurger(id) {
                const req = await fetch (`http://localhost:3000/burgers/${id}`, {
                    method: "DELETE"
                })

                const res = req.json()

                this.msg = ` Order number ${id} canceled successfully!`
                setTimeout(() => this.msg = "", 3000)

                this.getPedidos()
            },
            async updateBurger(event, id) {
                const option = event.target.value

                const dataJSON = JSON.stringify({ status:option })

                const req = await fetch (`http://localhost:3000/burgers/${id}`, {
                    method: "PATCH",
                    headers: {"Content-Type": "application/json" },
                    body: dataJSON
                })

                const res = await req.json()

                this.msg = `Order número ${res.id} has been updated to ${res.status}`
                setTimeout(() => this.msg = "", 3000)
            }
        },
        mounted() {
            this.getPedidos() 
        }
    }
</script>

<style scoped>
    #message {
        font-weight: bold;
        text-align: center;
        color: #363636;
        background-color: #A9A9A9;
        border: 2px solid #4F4F4F;
        border-radius: 5px;
        padding: 8px;
        max-width: 400px;
        margin: 56px auto;
    }

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