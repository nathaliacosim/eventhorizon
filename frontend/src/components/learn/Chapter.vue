<template>
    <div>
        <b-card :title="chapter.name" 
            img-src="https://conteudos.xpi.com.br/wp-content/uploads/2020/10/fundo-geometrico-de-tecnologia_29971-339.jpg"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-5 chapter">
           
            
            <p v-html="chapter.description"></p>
            <div class="chapter-button" v-if="questionLevel != 5">
                <b-button href="https://www.youtube.com/watch?v=3VLPyOLC1nc&list=PLPz6TqSYQzDYuQ3WqF5plmN0rycwcYULm&index=1" target="_blank" variant="primary">Conteúdo</b-button>
                <b-button @click="question" variant="success">Começar</b-button>
            </div>
             <div class="progress mt-5 mb-2">
                <div v-bind:class="{'progress-bar': true, 'bg-primary': questionLevel < 5, 'bg-warning': questionLevel == 5}"
                role="progressbar" v-bind:style="{width: questionLevel*20+'%'}" 
                aria-valuenow="25" aria-valuemin="0" aria-valuemax="100"></div>
            </div>
            <div class="d-flex flex-row-reverse">
                <div v-bind:class="{'question-level': true, 'progress-success': questionLevel == 5}">{{questionLevel}}</div>
            </div>
        </b-card>
    </div>
</template>

<script>
import axios from 'axios'
import {baseApiUrl} from '../../global'
import { mapState } from 'vuex'

export default {
    name: 'Chapter',
    props: ['chapter'],
    data: function (){
        return {
            questionLevel: 0
        }
    },
    computed: mapState(['user']),
    methods: {
        question(){
            const url = `${baseApiUrl}/user/${this.user.id}/chapter/${this.chapter.id}`
            axios.get(url)

            this.$router.push({
                name: 'questions',
                params: {id: this.chapter.id, level: this.questionLevel}
            })
        },
        getQuestionLevel(){
            const url = `${baseApiUrl}/user/${this.user.id}/chapter/${this.chapter.id}/questionLevel`
            axios.get(url).then(resp => {
                if (resp.data.questionLevel){
                    this.questionLevel = resp.data.questionLevel
                }
            })
        }
    },
    mounted(){
        this.getQuestionLevel()
    }
}
</script>

<style>
    .chapter {
        /* margin-bottom: 100px; */

        box-shadow: 0 10px 10px rgb(126 126 126 / 30%);
        transition: all .3s ease;
    }

    .chapter:hover {
        margin-top: 5px;
        box-shadow: none;
        cursor: pointer;
    }

    .chapter-button {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: stretch;
    }

    .question-level {
        color: #fff;
        font-size: 1.2rem;
        font-weight: 700;

        border: 2px solid #007BFF;
        border-radius: 20px;

        padding: 5px 15px;

        background-color: #007BFF;
    }

    .progress-success {
        background-color: #FFC100;
        border-color: #FFC100;
    }
</style>