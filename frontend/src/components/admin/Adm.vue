<template>
    <div class="adm d-flex flex-direction-row justify-content-center align-items-center">
        <div class="auth-container">
            <img src="../../assets/logo-pretoebranco-3.0.png" alt="Logomarca">
            <h1>Login — ADM</h1>
            <div class="form">
                <p>E-mail:</p>
                <input type="email" placeholder="Digite o seu e-mail..." v-model="user.email">
                <p>Senha:</p>
                <input type="password" placeholder="Digite a sua senha..." v-model="user.password">
            </div>
            <a href @click.prevent="signin" class="bg-primary">Entrar</a>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import {baseApiUrl, showError} from '../../global'

export default {
    name: 'Adm',
    data: function(){
        return {
            user: {}
        }
    },
    methods: {
        signin(){
            const url = `${baseApiUrl}/signin`
            axios.post(url, this.user).then(resp => {
                if (resp.data.admin){
                    this.$router.push({path: '/adm/dashboard'})
                } else {
                    showError('Este usuário não é administrador')
                }
            })
            // if (this.user.admin){
            //     this.$route.push({path: '/learn'})
            // } else {
            //     showError('Este usuário não é administrador')
            // }
        }
    }
}
</script>

<style>
    .adm {
        height: 100vh;
        background-color: #0D6EFD;
    }

    .auth-container img {
        height: 50px;
        margin-bottom: 10px;
    }
</style>