<template>
    <div class="module">
        <hr>
        <h1>{{module.name}}</h1>
        <div class="container">
            <div class="row">
                <div class="col-xl-6 col-sm-12" v-for="chapter in chapters" :key="chapter.id">
                    <Chapter :chapter="chapter"/>
                </div>
            </div>
        </div>
        <hr>
    </div>
</template>

<script>
import Chapter from './Chapter'

export default {
    name: 'Module',
    components: {Chapter},
    props: ['module'],
    data: function(){
        return {
            chapters: []
        }
    },
    methods: {
        getChapters(){
            this.chapters = this.module.chapters
        }
    },
    mounted(){
        this.getChapters()
    }
}
</script>

<style>
    .module h1{
        text-align: center;
        margin-bottom: 30px;
    }

    .module {
        padding: 20px;
    }
</style>