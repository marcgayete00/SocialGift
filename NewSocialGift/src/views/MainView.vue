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
              <a href=""> <img src="../../img/logo.png" id="logoNavBar" alt=""></a>
            </li>
            <li>
            <a href=""><i class="fa-solid fa-house"></i> Home</a>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-magnifying-glass"></i> Search</a>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-envelope"></i> Messages</a>
            </li>
            <li>
              <a href=""><i class="fa-sharp fa-solid fa-bell"></i> Notifications</a>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-pen-to-square"></i> Create</a>
            </li>
            <li id ="MoreLi">
              <a href="" onclick="openForm()"><i class="fa-solid fa-bars"></i> More</a>
            </li>
        </ul>
        </div>
        <div class="options-box">
          <div id="profile-box">
            <img class="profileimg" src="../../img/DefaultProfilePhoto.png">
            <h3>Pablo03</h3>
            <h5>Pablo García</h5>
          </div>
          <h3>Plantillas de listas</h3>
          <ul>
            <li><a href="#">Lista de Deseos</a></li>
            <li><a href="#">Lista de Cumpleaños</a></li>
            <li><a href="#">Lista Blanco y Negro</a></li>
          </ul>
        </div>
        <div class="image-section">
            <div>
              <div class="listheader">
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png">
                <h3>NickName</h3>
                <img class="moreimg" src="../../img/Mas.png">
              </div>
              <img class="imageslide" src="../../img/mainScrenshoot.png">
            </div>
            <div>
              <div class="listheader">
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png">
                <h3>NickName</h3>
                <img class="moreimg" src="../../img/Mas.png">
              </div>
              <img class="imageslide" src="../../img/mainScrenshoot.png">
            </div>
            <div>
              <div class="listheader">
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png">
                <h3>NickName</h3>
                <img class="moreimg" src="../../img/Mas.png">
              </div>
              <img class="imageslide" src="../../img/mainScrenshoot.png">
            </div>
            <div>
              <div class="listheader">
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png">
                <h3>NickName</h3>
                <img class="moreimg" src="../../img/Mas.png">
              </div>
              <img class="imageslide" src="../../img/mainScrenshoot.png">
            </div>
          </div>
      </section>

    </body>
  </template>

<style scoped src="../assets/mainStyle.css"></style>

  