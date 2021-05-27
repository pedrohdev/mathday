<template>
    <div class="container">
        <div class="box">
            <h1 class="title">Quiz em comemoração ao dia da matemática <br> 8º Tarde 🎉📐</h1>
            <div class="start">
                <button @click="$emit('start')">
                    Começar
                </button>
            </div>
        </div>
        <footer>
            Desenvolvido por: <br> <a href="https://www.github.com/pedrohdev">Henrique Vieira</a> e  <a href="https://github.com/cr3plovepython">João Alisson</a>
        </footer>
    </div>
</template>

<script>
export default {
    name: "Start"
}
</script>

<style scoped>
footer {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    text-align: center;
    padding-bottom: 18px;
}

h1 {
    text-align: center;
}

div.container {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

div.container > div.box {
    width: 100%;
    display: flex;
    flex-direction: column;
}

div.start {
    margin-top: 20px;
    display: flex;
    justify-content: center;
}

</style>