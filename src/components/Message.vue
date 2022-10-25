<template>
    <div class="message-container">
        {{msg}}
    </div>
</template>

<script>
    export default {
        name: 'Message',
        props: {
            msg: String
        }
    }
</script>

<style scoped>
    .message-container {
        color: #004085;
        background-color: #cce5ff;
        border: 2px solid #88daff;
        border-radius: 5px;
        padding: 8px;
        max-width: 400px;
        margin: 32px auto;
    }
</style>