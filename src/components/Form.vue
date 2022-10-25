<template>
    <div>
        <p>Componente de mensagem</p>
        <form id="form-create">
            <div class="input-container">
                <label for="name">Client name</label>
                <input type="text" id="name" name="name" placeholder="Type your name" v-model="name" >
            </div>

            <div class="input-container">
                <label for="bread">Choose the bread</label>
                <select name="bread" id="bread" v-model="bread">
                    <option disabled value="" > Select your bread </option>
                    <option v-for="bread in breads" :key="bread.id" :value="bread.tipo"> {{bread.tipo}} </option>
                </select>
            </div>

            <div class="input-container">
                <label for="meat">Choose your burguer meat</label>
                <select name="meat" id="meat" v-model="meat">
                    <option disabled value=""> Select your meat </option>
                    <option v-for="meat in meatData" :key="meat.id" :value="meat.tipo"> {{meat.tipo}} </option>
                </select>
            </div>

            <div id="options-container" class="input-container">
                <label id="options-title" for="options">Select the options</label>
                <div id="checkbox-container" v-for="option in optionsData" :key="option.id" >
                    <input type="checkbox" name="options" id="options" v-model="options" :value="option.tipo">
                    <span>{{option.tipo}}</span>
                </div>
            </div>

            <div class="input-container">
                <input type="submit" class="submit-btn" value="Create my burguer">
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'Form',
        data() {
            return {
                breads: null,
                meatData: null,
                optionsData: null,
                name: null,
                bread: null,
                meat: null,
                options: [],
                status: 'Requested',
                msg: null
            }
        },
        methods: {
            async getIngredients() {
                const req = await fetch("http://localhost:3000/ingredientes")

                const data = await req.json()

                this.breads = data.paes
                this.meatData = data.carnes
                this.optionsData = data.opcionais

            }
        },
        mounted() {
            this.getIngredients()
        }
    }
</script>

<style scoped>
    #form-create {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 24px;
    }

    label {
        font-weight: bold;
        margin-bottom: 16px;
        color: #222;
        padding: 4px 8px;
        border-left: 4px solid #FCBA03;
    }

    input, select {
        padding: 4px 8px;
        width: 300px;
    }

    #options-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #options-title {
        width: 100%;
    }

    #checkbox-container {
        width: 50%;
        display: flex;
        align-items: flex-start;
        margin-bottom: 16px;
    }

    #checkbox-container span,  #checkbox-container input {
        width: auto;
    }

    #checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
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

    .submit-btn:hover {
        background-color: #444;
        border: 2px solid #444;
        color: #fdc52a;
    }
</style>