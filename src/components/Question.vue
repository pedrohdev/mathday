<template>
    <div >
        <div v-if="concluded" class="container concluded">
            <canvas width="100%" height="100%" id="confetti"></canvas>

            <div class="back">
                <button @click="$emit('back')">Voltar</button>
            </div>

            <div v-if="score == questions.length">
                <h1 class="result" >Você ganhou 🥳</h1>
                <audio autoplay="autoplay" src="../assets/audio/win.mp3"></audio>
            </div>

            <div v-else>
                <h1 class="result">Você perdeu 😭</h1>
                <audio autoplay="autoplay" src="../assets/audio/fail.mp3"></audio>
            </div>

            <h1 class="score">{{score}}/{{questions.length}}</h1>
        </div>

        <div v-else class="container">
            <p v-html="questions[position].question" class="question">
            </p>
            <div class="answers">
                <div>
                    <button class="choices" v-for="(choice, index) in questions[position].choices" :key="choice" :class="{wrong: index != questions[position].answer && clicked}" @click="check(index)">
                        {{ choice }}
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import confetti from 'canvas-confetti'
import questions from '../database'

export default {
    name: "Question",
    data(){
        return {
            position: 0,
            questions,
            clicked: false,
            concluded: false,
            score: 0,
            confetti: ""
        }
    },
    methods: {
        check(index){
            if(index == this.questions[this.position].answer){
                this.score++
            }

            this.clicked = true
            
            setTimeout(() => {
                this.clicked = false

                if(this.questions[this.position+1]){
                    this.position++
                }else{
                    this.concluded = true
                    
                    if(this.score == this.questions.length){
                        this.confetti({
                            particleCount: 100,
                            spread: 160
                        })
                    }
                }
            }, 500)
        }
    },
    mounted(){
        this.confetti = confetti.create(document.querySelector("#confetti"), {
            resize: true,
            useWorker: true
        })
    }
}
</script>

<style scoped>
    div.back {
        display: flex;
        justify-content: center;
        margin-bottom: 50px;
    }

    div.back > button {
        width: 150px;
    }


    h1.result {
        font-size: 2.7rem;
        margin-bottom: 0;
        text-align: center;
    }

    h1.score {
        font-size: 2.5rem;
        text-align: center;
    }

    canvas#confetti {
        
        z-index: 2;
        position: absolute;
        pointer-events: none;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;

    }

    div.container {
        display: flex;
        flex-direction: column;
    }

    div.container.concluded{
        margin-top: 50px;
    }

    p.question {
        margin-top: 100px;
        font-weight: bold;
        font-size: 1.8rem;
        line-height: 2.5rem;
        text-align: center;
        margin-left: 10px;
        margin-right: 10px;
    }

    div.answers {
        margin-top: 20px;
        display: flex;
        justify-content: center;
        margin-bottom: 100px;
    }

    div.answers > div{
        width: 80%;
        display: flex;
        flex-direction: column;
    }


    button.choices {
        width: 100%;
        margin-top: 20px;
        background: rgb(119, 0, 255);
    }

    button.wrong {
        background: rgb(41, 41, 41);
    }

    button.wrong::after {
        content: '- Errado';
    }
</style>