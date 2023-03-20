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
        <div class="sidebar">
          <ul>
            <li><img id="logonav" src="../../img/logo.png"></li>
            <li><img class="iconnav" src="../../img/Home.png"><a href="#">Inicio</a></li>
            <li><img class="iconnav" src="../../img/Buscar.png"><a href="#">Buscar</a></li>
            <li><img class="iconnav" src="../../img/Mensaje.png"><a href="#">Mensajes</a></li>
            <li><img class="iconnav" src="../../img/Notificaciones.png"><a href="#">Notificaciones</a>
              <ul>
                <li><a href="#">Servicio 1</a></li>
                <li><a href="#">Servicio 2</a></li>
                <li><a href="#">Servicio 3</a></li>
              </ul>
            </li>
            <li><img class="iconnav" src="../../img/Crear.png"><a href="#">Crear</a></li>
            <li><img id="iconMas" src="../../img/Mas.png"><a id="aMas" href="#">Más</a></li>

          </ul>
        </div>
        </section>
    </body>
  </template>

<style scoped src="../assets/mainStyle.css"></style>

  