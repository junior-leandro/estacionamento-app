<template>
    <div class="mensagem-container">
        <h2>{{ msg }}</h2>
    </div>
</template>

<script>
export default {
    name: "Mensagem",

    props: {
        msg: String
    }
}
</script>

<style scoped>
.mensagem-container {
    color: white;
    background-color: red;
    border-radius: 8px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
}

.mensagem-container h2 {
    font-size: 20px;
    text-align: center;
}
</style>