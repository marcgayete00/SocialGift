<script>
import language from './../components/language.vue'

export default {
  components: {
    language
  },
  data() {
    
  },
  methods: {
    loginUser() {
      const user = {
        email: document.getElementById('email').value,
        password: document.getElementById('password').value
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
          window.location.href = 'main'
        })
        .catch((error) => {
          // Respuesta en caso de error de servidor
        })
    }
  }
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
              @keydown.enter="loginUser"
            /><br />
            <a id="loginButton" @click="loginUser"> Login </a>
            <hr />
            <!-- USAR ALTERNATIVA -->
            <span id="textRegister">¿No tienes cuenta? <a href="register"> Registrate</a></span>
          </form>
        </div>
      </section>

      <section id="ImageSection">
        <img id="backgroundImg" src="img/mainScrenshoot.png" />
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

  .profileimglist{
    margin-left: 10px !important;
  }


}
</style>

<style scoped>
@import '../assets/HomeStyle.css';
</style>
