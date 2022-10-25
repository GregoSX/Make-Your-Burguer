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
                    <option value=""> Select your bread </option>
                    <option value="brown">Brown bread</option>
                </select>
            </div>

            <div class="input-container">
                <label for="meat">Choose your burguer meat</label>
                <select name="meat" id="meat" v-model="meat">
                    <option value=""> Select your meat </option>
                    <option value="steak">Rump steak</option>
                </select>
            </div>

            <div id="options-container" class="input-container">
                <label id="options-title" for="options">Select the options</label>
                <div id="checkbox-container">
                    <input type="checkbox" name="options" id="options" v-model="options" value="salami">
                    <span>Salami</span>
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