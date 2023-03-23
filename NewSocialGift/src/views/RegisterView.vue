<script setup>
import language from './../components/language.vue'
</script>

<template>
  <div>
    <language />
    <section id="GeneralSectionRegister">
      <section id="RegisterSection">
        <div>
          <img src="img/logo.png" id="LogoStyle" />
          <form>
            <input type="text" class="inputRegister" name="username" placeholder="Usuario..." /><br/>
            <input type="text" class="inputRegister" name="surname" placeholder="Surname..." /><br/>
            <input type="text" class="inputRegister" name="email" placeholder="E-mail..." /><br/>
            <input type="password" class="inputRegister" id="password" name="password" placeholder="Contraseña..."/><br/>
            <button type="submit" id="pPhotoButton"><a href="main"> Profile photo </a></button>
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
      width: 2px;
      height: 2px;
    }

    #GeneralSectionRegister {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    #RegisterSection {
      margin-top: 20px;
    }
    
    .inputRegister {
      width: 20px;
      height: 30px;
      border-radius: 5px;
      border: 1px solid #000000;
      margin-top: 10px;
    }

    #GeneralSectionRegister2 {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    #RegisterSection2 {
      margin-top: 400px;
      
    }
    #registerFooter {
      display: none;
    }
    
  }
   
  </style>

<style scoped>
@import '../assets/HomeStyle.css';
</style>
