<template>
    <div class="p">
      <center>
        <h1>Bienvenidos a la app de tareas</h1>
        <p>Esta es una aplicación que permite gestionar las tareas de los estudiantes</p>
        <h3>Login</h3>
  
        <v-card
        height="230"
        width="450"
      >
        <div>
  
        <v-responsive    class="mx-auto"    max-width="344" >
        <v-text-field class="my-custom-text-field" label="Email address"  placeholder=""  type="email" variant="solo-filled" padding-top="100"></v-text-field>
        </v-responsive>
             
        <v-responsive    class="mx-auto"    max-width="344"  >
        <v-text-field label="Password" type="password" variant="solo-filled"></v-text-field>
      
        </v-responsive>
        <v-btn variant="tonal">
        Iniciar
        </v-btn>
  
  
      </div>
    </v-card>
  
        <a href="/tareas">Click para iniciar (sin nuxtLink)</a>
  <br>
  <br>
        <NuxtLink to="/tareas">
          Click para iniciar (Con nuxtLink)
        </NuxtLink>
      </center>
  
    </div>
  </template>

<style>
.my-custom-text-field {
  padding-top: 20px;
}

</style>
