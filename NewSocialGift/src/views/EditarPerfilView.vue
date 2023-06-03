<script setup>
import language from './../components/language.vue'
import NavBar from './../components/NavBar.vue'
import MiComponente from './../components/separarTrama.vue'

const token = localStorage.getItem('accessToken')
const flag = true;

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
      document.getElementById('input_profile_photo').placeholder = data.image
    })
    .catch((error) => {
      //Respuesta en caso de error de servidor
    })
}

function verifyPassword( password, new_password, new_password2, email ){
  console.log( password, new_password, new_password2, email)
  if (new_password != new_password2) {
    alert('The new passwords do not match')
    flag = false;
    return Promise.resolve(false);

  } else {
    const user = {
      email: email,
      password: password
    }

    return fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(user)
    })
      .then((response) => {
        if (response.status === 200) {
          return true;
        } else {
          return false;
        }
      })
      .catch((error) => {
        console.log(error)
        return false;
      })
  }

}


async function editData() {
  const password = document.getElementById('current_password').value
  const new_password = document.getElementById('new_password').value
  const new_password2 = document.getElementById('new_password2').value
  const email = document.getElementById('input_email').placeholder

  //Verficar si la contraseña introducida es correcta
  if (await verifyPassword(password , new_password , new_password2, email)){
    
    const name = document.getElementById('input_name').value
    const last_name = document.getElementById('input_last_name').value
    const email = document.getElementById('input_email').value
    const image = document.getElementById('input_profile_photo').value


    if (name === undefined){
      name = document.getElementById('input_name').placeholder
    }

    if (last_name === undefined){
      last_name = document.getElementById('input_last_name').placeholder
    }

    if (email === undefined){
      email = document.getElementById('input_email').placeholder
    }

    if(image === undefined){
      image = document.getElementById('input_profile_photo').placeholder
    }

    const user = {
      name: name,
      last_name: last_name,
      email: email,
      password: password,
      image: image
    }

    fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/users', {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${token}`
      },
      body: JSON.stringify(user)
    })
      .then((response) => {
        if (response.status === 200) {
          alert('User edited correctly')
          window.location.href = '/editarperfil'
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
    
    } else {
      if (flag){
        alert('The current password is incorrect')
      }
    }
}

function deleteAccount(){
  fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/users', {
      method: 'DELETE',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${token}`
      }
    })
      .then((response) => {
        if (response.status === 200) {
          alert('User edited correctly')
          localStorage.removeItem('accessToken')
          window.location.href = '/'
        } else {
          switch (response.status) {
            case 401:
              alert('Unauthorized')
              break
            case 500:
              alert('User not deleted')
              break
            case 502:
              alert('Internal server error')
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

  function toggleTaskBar(){
      const navigation = document.querySelector('.navigation');
      if (navigation) {
        navigation.style.display = 'block';
      }
    } 
</script>

<template>
  <language />
  <a @click="toggleTaskBar()" class="togleNavBar" ><i class="fa-solid fa-bars"></i></a>
  <section id="GeneralSection">
    <NavBar />
    <section class="editarperfil-section">
      <h2 id="tituloeditarperf">Editar Perfil</h2>
      <div>
        <div id="headeditarperfil">
          <img id="profileImageJS" src="" />

          <h3 id="usernameJS"></h3>
          <a href="#"><button id="EliminarButton" @click="deleteAccount">Eliminar Cuenta</button></a>
        </div>
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
        <div class="diveditarperfil">
          <h3>URL profile photo</h3>
          <input type="text" id="input_profile_photo" placeholder="" />
        </div>
        <div id="changePassword"> 
          <h3>Cambiar Contraseña</h3>
          <input type="password" id="current_password" placeholder="*******" />
          <input type="password" id="new_password" placeholder="New password" />

          <input type="password" id="new_password2" placeholder="Retype new password" />
          <a href="#"><button @click="editData" id="GuardarButton">Guardar</button></a>
        </div>
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
    width: 100% !important;
    height: 100% !important;
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
    position: relative !important;
    top: 10px !important;
    margin-left: 100px !important;
  }
  #headeditarperfil{
    position: relative !important;
    top: -90px !important;
  }

  #profileImageJS{
    width: 100px !important;
    height: 100px !important;
    margin-left: 10px !important;
  }

  #EliminarButton{
    margin-left: 40px !important;
    margin-top: 10px !important;
    width: 150px !important;
    font-size: 15px !important;
  }

  .diveditarperfil{
    position: relative !important;
    margin-left: 10px !important;
    top: -70px !important;
  }

  .diveditarperfil h3{
    margin-top: 10px !important;
    font-size: 15px !important;
  }

  .diveditarperfil input{
    width: 150px !important;
    position: relative !important;
    top: 2px !important;
  }

  #changePassword{
    position: relative !important;
    top: -70px !important;
    margin-left: 10px !important;
  }

  #changePassword input{
    width: 150px !important;
  }

  #new_password{
    position: relative !important;
    top: 20px !important;
    margin-left: 305px !important;
  }

  #new_password2{
    position: relative !important;
    top: -40px !important;
  }

}
</style>
