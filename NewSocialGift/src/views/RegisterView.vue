<template>
  <body>
    <section id="LanguageSection">
      <nav>
        <ol id="LanguageList">
          <li>
            <img id="switchImg" src="../components/icons/ds.png" />
          </li>
          <li id="switchLi">
            <label class="switch">
              <input type="checkbox" />
              <span class="slider"></span>
            </label>
          </li>
          <li>
            <select name="select" id="LanguageSelect">
              <option value="value1" selected>Spanish</option>
              <option value="value2">English</option>
            </select>
          </li>
        </ol>
      </nav>
    </section>
    
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
  </body>

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

<style scoped src="../assets/HomeStyle.css"></style>
