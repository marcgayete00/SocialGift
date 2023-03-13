<template>
  <body>
    <section id="LanguageSection">
      <nav>
        <ol>
          <li>Idioma</li>
          <li>
            <select name="select" id="LanguageSelect">
              <option value="value1">Spanish</option>
              <option value="value2" selected>I</option>
              <option value="value3">Value 3</option>
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
            <input type="text" class="input" name="username" placeholder="Usuario" /><br />
            <input
              type="password"
              class="input"
              id="password"
              name="password"
              placeholder="Contraseña"
            /><br />
            <button type="submit" id="loginButton">Login</button>
            <hr />
            <span id="textRegister">¿No tienes cuenta? <a href="#">Registrate</a></span>
          </form>
        </div>
      </section>

      <section id="ImageSection">
        <img src="img/mainScrenshoot.png" />
      </section>
    </section>
  </body>
</template>

<style scoped src="../assets/HomeStyle.css"></style>

