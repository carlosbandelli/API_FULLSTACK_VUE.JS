<template>
   <div class="columns  is-centered  "> 
    <div>
        <div>
        <br>
        <h1>Ações</h1>
        <br>
        <table class="table">          
                    
          <th><router-link :to="{name: 'Register'}"><button class="button is-success">Registar</button> </router-link></th>  
          <th><router-link :to="{name: 'Users'}"><button class="button is-info">Painel de usuarios</button> </router-link></th>
          <th><router-link :to="{name: 'Login'}"><button class="button is-link">Trocar de usuario</button> </router-link></th>            
                     
        </table>
        </div>

        </div>      
 
                      
        </div>
</template>

<script>
// @ is an alias to /src

export default {
  
}
</script>
