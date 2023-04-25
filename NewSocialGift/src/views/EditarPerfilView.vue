<script setup>
import language from './../components/language.vue'
import NavBar from './../components/NavBar.vue'

const token = localStorage.getItem('accessToken')
const email = localStorage.getItem('email')
if (token === undefined || token === null) {
  window.location.href = '/'
} else {
    //Hacer una peticion GET pasandole el email del usuario logueado
    //Cambiar el @ de la variable email por URL encoded %40
    const encodedEmail = encodeURIComponent(email).replace('@', '%40');
  
  fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/search?s=${encodedEmail}`, {
    method: 'GET',
    headers: {
        'Authorization': `Bearer ${token}`
    }
  })
    .then((response) => {
      if (response.status === 200) {
        return response.json()
      } 
    })
    .then((data) => {
      //mostrar el cotenido que nos devuelve el servidor
      console.log(data);
      
    })
    .catch((error) => {
      //Respuesta en caso de error de servidor
    })
}
</script>

<template>
  <language />

  <section id="GeneralSection">
    <NavBar />
    <section class="editarperfil-section">
      <h2 id="tituloeditarperf">Editar Perfil</h2>
      <div>
        <div id="headeditarperfil">
          <img src="../../img/DefaultProfilePhoto.png" />
          <h3>NickName</h3>
          <a href="#"><button id="EliminarButton">Eliminar Cuenta</button></a>
        </div>
        <a href="#"><h4>Cambiar Foto</h4></a>
        <div class="diveditarperfil">
          <h3>Nombre</h3>
          <input type="text" id="input_name" placeholder="Nombre" />
        </div>
        <div class="diveditarperfil">
          <h3>Last Name</h3>
          <input type="text" id="input_last_name" placeholder="Last Name" />
        </div>
        <div class="diveditarperfil">
          <h3>Email</h3>
          <input type="text" id="input_email" placeholder="Email" />
        </div>
        <div class="diveditarperfil">
          <h3 id="titulocont">Cambiar Contraseña</h3>
          <button>******</button>
        </div>
        <a href="#"><button id="GuardarButton">Guardar</button></a>
      </div>
    </section>
  </section>
</template>

<style scoped>
@import '../assets/EditarPerfilStyle.css';
</style>

<style>
@media screen and (max-width: 600px) {
  .editarperfil-section {
    margin-top: 50px !important;
    width: 105% !important;
  }
  .editarperfil-section > div {
    margin-top: 20px !important;
    margin-left: 0px !important;
  }

  .editarperfil-section img {
    width: 100px !important;
  }

  .editarperfil-section button {
    width: 100px !important;
    font-size: 15px !important;
  }

  .editarperfil-section select {
    padding: 10px !important;
  }
  .diveditarperfil textarea {
    width: 175px !important;
  }
  .editarperfil-section h4 {
    margin-top: 0px !important;
    display: flex !important;
  }
  .editarperfil-section h2 {
    visibility: hidden;
  }
  #GuardarButton {
    margin-left: 140px !important;
  }
}
</style>
