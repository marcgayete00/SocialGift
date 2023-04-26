<script setup>
import language from './../components/language.vue'
import NavBar from './../components/NavBar.vue'
import MiComponente from './../components/separarTrama.vue'

const token = localStorage.getItem('accessToken')
console.log('Token2 ' + token)

if (token === undefined || token === null) {
  window.location.href = '/'
} else {
  //llamar a la funcion que separa
  const id = MiComponente.methods.obtenerIdDesdeToken(token)
  //Hacer una peticion GET pasandole el email del usuario logueado

  fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${id}`, {
    method: 'GET',
    headers: {
      Authorization: `Bearer ${token}`
    }
  })
    .then((response) => {
      if (response.status === 200) {
        return response.json()
      }
    })
    .then((data) => {
      //mostrar el cotenido que nos devuelve el servidor
      document.getElementById('usernameJS').innerHTML = data.name
      document.getElementById('input_name').placeholder = data.name
      document.getElementById('input_last_name').placeholder = data.last_name
      document.getElementById('input_email').placeholder = data.email
      document.getElementById('profileImageJS').src = data.image
    })
    .catch((error) => {
      //Respuesta en caso de error de servidor
    })
}

function editData() {
  const id = MiComponente.methods.obtenerIdDesdeToken(token)
  const name = document.getElementById('input_name').value
  const last_name = document.getElementById('input_last_name').value
  const email = document.getElementById('input_email').value
  const password = document.getElementById('current_password').value
  const image =
    'https://balandrau.salle.url.edu/i3/repositoryimages/photo/47601a8b-dc7f-41a2-a53b-19d2e8f54cd0.png'

  const user = {
    id: id,
    name: name,
    last_name: last_name,
    email: email,
    password: password,
    image: image
  }

  fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/users', {
    method: 'PUT',
    headers: {
      Authorization: `Bearer ${token}`
    },
    body: JSON.stringify(user)
  })
    .then((response) => {
      if (response.status === 200) {
        alert('User edited correctly')
      } else {
        switch (response.status) {
          case 400:
            alert('Bad request')
            break

          case 401:
            alert('Unauthorized')
            break

          case 406:
            alert('Missing parameters')
            break

          case 409:
            alert('The email address has already been previously registered')
            break

          case 410:
            alert('No user has been edited')
            break

          default:
            alert('An error has occurred')
            break
        }
      }
    })
    .catch((error) => {
      console.log(error)
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
          <img id="profileImageJS" src="" />

          <h3 id="usernameJS"></h3>
          <a href="#"><button id="EliminarButton">Eliminar Cuenta</button></a>
        </div>
        <a href="#"><h4>Cambiar Foto</h4></a>
        <div class="diveditarperfil">
          <h3>Nombre</h3>
          <input type="text" id="input_name" placeholder="" />
        </div>
        <div class="diveditarperfil">
          <h3>Last Name</h3>
          <input type="text" id="input_last_name" placeholder="" />
        </div>
        <div class="diveditarperfil">
          <h3>Email</h3>
          <input type="text" id="input_email" placeholder="" />
        </div>
        <h3>Cambiar Contraseña</h3>
        <input type="text" id="current_password" placeholder="*******" />
        <input type="text" id="new_password" placeholder="New password" />

        <input type="text" id="new_password2" placeholder="Retype new password" />
        <a href="#"><button @click="editData" id="GuardarButton">Guardar</button></a>
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
