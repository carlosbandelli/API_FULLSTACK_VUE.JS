<template>
    
    <div class="columns  is-centered  ">
        <div>
        <div>
        <br>
        <h1>Painel Adm</h1>
        <div>
            <p>User</p>
        </div>
            <table class="table">
            <thead>
                <tr>      
                <th>Nome</th>      
                <th>E-mail</th>
                <th>Cargo</th>
                <th>Ações</th>  
                </tr>
            </thead>  
            <tbody>
                <tr v-for="user in users" :key="user.id">
                    <td>{{user.name}}</td>
                    <td>{{user.email}}</td>
                    <td>{{user.role | processRole }}</td>
                    <td>
                        <router-link :to="{name: 'UserEdit', params: {id: user.id}}"><button class="button is-success">Editar</button> </router-link>|
                        <button class="button is-danger" @click="showModalUser(user.id)">Deletar</button>
                    </td>
                </tr>

            </tbody>
           
            </table>              
              <router-link :to="{name: 'Home'}"><button class="  button is-primary ">Home</button> </router-link>
        </div>

        </div>

        <div  :class="{modal: true, 'is-active': showModal}">
                    <div class="modal-background"></div>
                    <div class="modal-content">
                       <div class="card">
                        <header class="card-header">
                            <p class="card-header-title">
                            Você quer realmente deletar esse usuário?
                            </p>                         
                        </header>
                        <div class="card-content">
                            <div class="content">
                            
                            </div>
                        </div>
                        <footer class="card-footer">                            
                            <a href="#" class="card-footer-item" @click="hideModal()">Cancelar</a>
                            <a href="#" class="card-footer-item" @click="deleteUser()">Sim, quero deletar!</a>
                        </footer>
                        </div> 
                    </div>
                    <button class="modal-close is-large" aria-label="close" @click="hideModal()"></button>
                    </div>
        
    </div>    
</template>

<script>
import axios from 'axios'
export default {
    created(){

        var req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
            } 
        }

        axios.get("http://localhost:8686/user",req).then(res => {
            console.log(res)
            this.users = res.data
        }).catch(err =>{
            console.log(err)
        })
        console.log("OLÀ!")
    },
    data(){
        return{
            users:[],
            showModal: false,
            deleteUserId: -1,
        }
    },

    methods: {
        hideModal(){
            this.showModal = false
        },

        showModalUser(id){
            this.deleteUserId = id
            this.showModal = true
        },

        deleteUser(){

             var req = {
                    headers: {
                        Authorization: "Bearer " + localStorage.getItem('token')
                    } 
                }

            axios.delete("http://localhost:8686/user/"+this.deleteUserId, req).then(res => {
                console.log(res)
                this.showModal = false
                this.users = this.users.filter(u => u.id != this.deleteUserId)
            }).catch(err => {
                console.log(err)
                this.showModal = false
            })
        }

    },

    filters: {
        processRole: function(value){
            if(value == 0){
                return "Usuario comum"
            }else if(value == 1){
                return "Admin"
            }
        }
    }

    
}
</script>

<style scoped>

</style>