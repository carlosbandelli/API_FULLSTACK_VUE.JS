<template>
    <div>
        <h2>Regitro de usuário</h2>
        <hr>
        <div class="columns  is-centered">
            <div class="column is-half"> 
                <div v-if="error != undefined">
                    <div class="notification is-danger is-light">                        
                        {{error}}
                    </div>                    
                </div>
                <p>Nome</p>
                <input type="text" placeholder="Nome do usuário" class="input" v-model="name"> 
                <p>E-mail</p>
                <input type="email" placeholder="email@email.com" class="input" v-model="email">   
                <p>Password</p>
                <input type="password" placeholder="*********" class="input" v-model="password">  
                <hr> 
                <button class="button is-success" @click="register">Cadastrar</button>  | 
                <router-link :to="{name: 'Users'}"><button class="button is-info">Painel de usuarios</button> </router-link>
            </div>
        </div>        
    </div>
</template>

<script>
import axios from 'axios'
export default {

    data(){
        return {
            name: '',
            password: '',
            email: '',
            error: undefined,
        }
    },
    methods:{
        register(){
            axios.post("http://localhost:8686/user",{
                name: this.name,
                password: this.password,
                email: this.email
            }).then(res => {
                console.log(res)
                this.$router.push({name: 'Home'})
            }).catch(err => {
                var msgErro = err.response.data.err
                this.error = msgErro
            })            
        }
    }  

}
</script>

<style scoped>

</style>