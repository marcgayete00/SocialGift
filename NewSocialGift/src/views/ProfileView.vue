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
      </section>

        <!--Mostrar perfil-->
        <section id="ProfileSection">
          <div>
            <div id="ProfileInfo">
              <div id="ProfileImage">
                <img  src="img/DefaultProfilePhoto.png" />
              </div>
              <div id="ProfileName">
                <h1>Pablo03</h1>
              </div>
              <div id="UserCount">
                <h1>6</h1><h3>Listas</h3>
                <h1>340</h1><h3>Amigos</h3>
              </div>
              <div id="ProfileDescription">
                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. del usuario</p>
              </div>
            </div>
          </div>
        </section>
        <hr>

        <section>
          <div id="SelectList">
            <a href="#" id="Lists">List</a>
            <a href="#" id="Lists">WishList</a>
          </div>

        </section>
        <section id="PostSection">
          <div class="grid-container">
            <div class="grid-item">1</div>
            <div class="grid-item">2</div>
            <div class="grid-item">3</div>
            <div class="grid-item">4</div>
            <div class="grid-item">5</div>
            <div class="grid-item">6</div>
          </div>
        </section>
        
    </body>
  </template>

<style scoped src="../assets/ProfileStyle.css"></style>

  