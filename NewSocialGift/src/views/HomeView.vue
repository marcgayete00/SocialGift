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
  </body>
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

<style scoped src="../assets/HomeStyle.css"></style>
