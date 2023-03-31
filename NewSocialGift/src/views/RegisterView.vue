<script setup>
import language from './../components/language.vue'
</script>

<template>
  <div>
    <language :show-hamburguer-menu="false" />
    <section id="GeneralSectionRegister">
      <section id="RegisterSection">
        <div>
          <img src="img/logo.png" id="LogoStyle" />
          <form>
            <input type="text" class="inputRegister" name="username" placeholder="Usuario..." /><br/>
            <input type="text" class="inputRegister" name="surname" placeholder="Surname..." /><br/>
            <input type="text" class="inputRegister" name="email" placeholder="E-mail..." /><br/>
            <input type="password" class="inputRegister" id="password" name="password" placeholder="Contraseña..."/><br/>

            <div class="file-upload-wrapper">
              <button type="button" class="upload-btn" onclick="document.getElementById('file-upload').click();">Profile photo</button>
              <input type="file" id="file-upload" name="file" accept="image/*">
            </div>

            <button type="submit" id="registerButton"><a href="main"> Siguiente </a></button>
          </form>
        </div>
      </section>
    </section>

    <section id="GeneralSectionRegister2">
      <section id="RegisterSection2">
        <span id="textRegister2">¿You have already an account?<a href="/"> Log-in</a></span>
      </section>
    </section>
  </div>

  <footer id="registerFooter">
    <div>
      <nav>
        <ol class="footerList2">
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
    #LogoStyle{
      width: 200px !important;
      height: 60px !important;
      margin-left: 50px !important;
      margin-top: 20px;
    }

    #GeneralSectionRegister {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    #RegisterSection {
      width: 300px;
      margin-top: 20px;
    }
    
    .inputRegister{
      width: 280px !important;
      margin-right: 20px;
    }

    #GeneralSectionRegister2 {
      display: flex;
      flex-direction: column;
      align-items: center;
      width: 350px;
      margin-bottom: 50px !important;
    }

    #RegisterSection2 {
      margin-top: 400px;
    }
    #registerFooter {
      display: none;
    }

    .upload-btn {
      width: 250px !important;
    }

    .file-upload-wrapper{
      margin-left: 25px !important;
    }

    #registerButton {
      width: 250px !important;
      height: 50px !important;
      margin-left: 25px !important;
      margin-bottom: 30px;
    }

    #RegisterSection2 {
      width: 210% !important;
      height: 30% !important;
      margin-top: 250px !important;
      padding-top: 7px !important;

    }

    #textRegister2{
     font-size: small !important;
     margin-left: 20px !important;
     padding-bottom: 10px !important;
    }

    #textRegister2 a{
      font-size: large !important;

    }
    
  }
   
  </style>

<style scoped>
@import '../assets/HomeStyle.css';
</style>
