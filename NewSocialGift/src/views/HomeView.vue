<script setup>
import language from './../components/language.vue'
</script>

<template>
  <div>
    <language />
    <section id="GeneralSection">
      <section id="LoginSection">
        <div>
          <img src="img/logo.png" id="LogoStyle" />
          <form>
            <input type="text" class="input" name="username" placeholder="Usuario" /><br/>
            <input
              type="password"
              class="input"
              id="password"
              name="password"
              placeholder="Contraseña"/><br/>
            <button type="submit" id="loginButton"><a href="main"> Login </a></button>
            <hr />
            <span id="textRegister">¿No tienes cuenta? <a href="register"> Registrate</a></span>
          </form>
        </div>
      </section>

      <section id="ImageSection">
        <img src="img/mainScrenshoot.png" />
      </section>
    </section>
  </div>
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
      }
      #ImageSection {
        display: none;
      }
      #loginFooter {
        display: none;
      }
    }
  </style>

<style scoped>
@import '../assets/HomeStyle.css';
</style>
