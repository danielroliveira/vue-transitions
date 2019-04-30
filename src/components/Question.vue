<template>
    <div class="question">
        <span class="pergunta">{{ pergunta }}</span>
        <ul class="answers">
            <li v-for="(resposta, i) in respostas" :key="i"
                @click="onEscolher(resposta.correct)">
                <span class="number">{{ i + 1 }}</span>
                <span class="text">{{ resposta.text }}</span>
            </li>
        </ul>
    </div>
</template>

<script>
import questions from "../util/questions";

export default {
    data(){
		return {
			pergunta: '',
			perguntaItem: 0,
			questions,
            respostas: [],
		}
	},
	methods: {
		obterPegunta(){
			let quant = this.questions.length
			this.perguntaItem ++

			if(this.perguntaItem === quant) {
				this.perguntaItem = 0
			}
			
			this.pergunta = this.questions[this.perguntaItem].text
			this.respostas = this.questions[this.perguntaItem].answers
		},
		onEscolher(correct){
            this.mycorrect = correct
            this.$emit('onEscolher', correct)
            setTimeout(() => {
                this.obterPegunta()
            }, 1000);
        }
    },
	created(){
		this.obterPegunta()
    },

}
</script>

<style>
    .question {
        height: 400px;
        color: #000;
        background-color: #FFF;
        width: 70%;
        border-radius: 20px;
        font-size: 2.5rem;

        display: flex;
        flex-direction: column;
        justify-content: space-around;
    }

    ul.answers {
        font-size: 2rem;
        padding: 0;
        display: flex;
        justify-content: space-around;
        flex-wrap: wrap;
    }

    .answers li {
        margin: 20px;
        background-color: #89c454;
        border-radius: 8px;
        width: 40%;

        display: flex;
        cursor: pointer;
    }

    .answers .number {
        padding: 10px;
        background-color: #1e9c31;
        color: #FFF;
        flex-basis: 30px;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
        user-select: none;
    }

    .answers .text {
        flex: 1;
        align-self: center;
        user-select: none;
    }
</style>
