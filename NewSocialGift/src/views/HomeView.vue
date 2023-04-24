<script setup>
import language from './../components/language.vue'

//Link apis
//https://balandrau.salle.url.edu/i3/socialgift/api-docs/v1/  (Api usuarios)
//https://balandrau.salle.url.edu/i3/mercadoexpress/api-docs/v1/ (Api productos)

//Obtener texto del input username
</script>

<script>
function loginUser() {
  var email = document.getElementById('email').value
  var password = document.getElementById('password').value

  const user = {
    email: email,
    password: password
  }

  fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/login', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(user)
  })
    .then((response) => {
      if (response.status === 200) {
        alert('User Logged In')
        return response.json()
      } else {
        switch (response.status) {
          case 404:
            alert('An error has occurred')
            break

          case 401:
            alert('Wrong email or password')
            break

          case 406:
            alert('Missing parameters')
            break
        }
      }
    })
    .then((data) => {
      const token = data.accessToken
      console.log(token)
      // Almacenar el token en localStorage
      localStorage.setItem('accessToken', token)
      localStorage.setItem('email', user.email)
      window.location.href = 'main'
    })
    .catch((error) => {
      //Respuesta en caso de error de servidor
    })
}
</script>

<template>
  <div>
    <language :show-hamburguer-menu="false" />
    <section id="GeneralSection">
      <section id="LoginSection">
        <div>
          <img src="img/logo.png" id="LogoStyle" />
          <form>
            <input type="text" class="input" id="email" placeholder="Email" /><br />
            <input
              type="password"
              class="input"
              id="password"
              name="password"
              placeholder="Contraseña"
            /><br />
            <button id="loginButton" @click="loginUser"><a href="#"> Login </a></button>
            <hr />
            <!-- USAR ALTERNATIVA -->
            <span id="textRegister">¿No tienes cuenta? <a href="register"> Registrate</a></span>
          </form>
        </div>
      </section>

      <section id="ImageSection">
        <img src="img/mainScrenshoot.png" />
      </section>
    </section>
    <footer id="loginFooter">
      <div>
        <nav>
          <ol class="footerList">
            <li><a href="#">Help</a></li>
            <li><a href="#">Privacy</a></li>
            <li><a href="#">Terms</a></li>
          </ol>
        </nav>
      </div>
    </footer>
  </div>
</template>

<style>
@media screen and (max-width: 600px) {
  #GeneralSection {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #LoginSection {
    margin-top: 20px;
    width: auto;
    padding-right: 30px !important;
  }
  #ImageSection {
    display: none;
  }
  #loginFooter {
    display: none;
  }

  #textRegister {
    display: flex;
    justify-content: center;
  }

  #LogoStyle {
    display: flex;
    justify-content: center;
    margin-left: 60px !important;
  }
}
</style>

<style scoped>
@import '../assets/HomeStyle.css';
</style>
