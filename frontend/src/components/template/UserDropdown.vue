<template>
    <div class="user-dropdown">
        <div class="user-button">
            <span>{{user.name}}</span>
            <div class="user-dropdown-img">
                <Gravatar :email="this.user.email" alt="User"/>
            </div>
            <i class="fa fa-angle-down"></i>
        </div>
        <div class="user-dropdown-content">
            <router-link to="/config"><i class="fa fa-cog"></i> Configuração</router-link>
            <router-link v-if="user.admin" to="/adm/dashboard"><i class="fa fa-bar-chart" aria-hidden="true"></i> Administração</router-link>
            <a @click.prevent="logout" href><i class="fa fa-sign-out"></i> Sair</a>
        </div>
    </div>
</template>

<script>
import Gravatar from 'vue-gravatar'
import {mapState} from 'vuex'
import {userKey} from '../../global'

export default {
    name: 'UserDropdown',
    components: {Gravatar},
    computed: mapState(['user']),
    methods: {
        logout(){
            localStorage.removeItem(userKey)
            this.$store.commit('setUser', null)
            this.$router.push({name: 'home'})
        }
    }
}
</script>

<style>
    .user-dropdown {
        height: 100%;
        position: relative;
    }

    .user-button {
        display: flex;
        align-items: center;
        color: #000;
        font-weight: 100;
        height: 100%;
        padding: 0px 20px;
    }

    .user-dropdown:hover {
        background-color: rgba(0, 0, 0, 0.2);
    }

    .user-dropdown-img {
        margin: 0px 10px;
    }

    .user-dropdown-img > img {
        max-height: 37px;
        border-radius: 5px;
    }

    .user-dropdown-content {
        position: absolute;
        right: 0px;
        background-color: #f9f9f9;
        min-width: 170px;
        box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
        padding: 10px;
        z-index: 1;

        display: flex;
        flex-direction: column;
        flex-wrap: wrap;

        visibility: hidden;
        opacity: 0;
        transition: visibility 0s, opacity 0.5s linear;
    }

    .user-dropdown:hover .user-dropdown-content {
        visibility: visible;
        opacity: 1;
    }

    .user-dropdown .user-dropdown-content a {
        text-decoration: none;
        color: #000;
        padding: 10px;
    }
    .user-dropdown .user-dropdown-content a:hover {
        background-color: #EDEDED;
        color: #000;
        padding: 10px;
    }

    /* Responsividade */

    @media (max-width: 415px){
        .user-dropdown .user-button {
            font-size: 0.6rem;
        }

        .user-dropdown-img > img {
            max-height: 20px;
            border-radius: 5px;
        }

        .user-button {
            padding: 0px;
        }
    }
</style>