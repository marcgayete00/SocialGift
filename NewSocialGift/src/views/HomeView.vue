<script setup>
import language from './../components/language.vue'

//Obtener texto del input username
var username = document.getElementById('username')
var password = document.getElementById('password')

//Obtener el boton de login
var loginButton = document.getElementById('loginButton')
</script>

<template>
  <div>
    <language :show-hamburguer-menu="false" />
    <section id="GeneralSection">
      <section id="LoginSection">
        <div>
          <img src="img/logo.png" id="LogoStyle" />
          <form>
            <input type="text" class="input" name="username" placeholder="Usuario" /><br />
            <input
              type="password"
              class="input"
              id="password"
              name="password"
              placeholder="Contraseña"
            /><br />
            <button type="submit" id="loginButton"><a href="main"> Login </a></button>
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
