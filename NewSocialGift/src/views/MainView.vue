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
        <div class="navigation">
        <ul>
            <li>
            <a href="#">Inicio</a>
            </li>
            <li>
            <a href="#">Sección 1</a>
            <ul>
                <li><a href="#">Opción 1</a></li>
                <li><a href="#">Opción 2</a></li>
                <li><a href="#">Opción 3</a></li>
            </ul>
            </li>
            <li>
            <a href="#">Sección 2</a>
            <ul>
                <li><a href="#">Opción 1</a></li>
                <li><a href="#">Opción 2</a></li>
                <li><a href="#">Opción 3</a></li>
            </ul>
            </li>
            <li>
            <a href="#">Sección 3</a>
            </li>
        </ul>
        </div>
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

<script type="javascript">
    var toggles = document.querySelectorAll('.navigation > ul > li > a');
    for (var i = 0; i < toggles.length; i++) {
    toggles[i].addEventListener('click', function(e) {
        e.preventDefault();
        var parent = this.parentNode;
        if (parent.classList.contains('active')) {
        parent.classList.remove('active');
        } else {
        parent.classList.add('active');
        }
    });
    }

</script>

<style scoped src="../assets/MainStyle.css"></style>

  