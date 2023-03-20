
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
            <li id ="MoreLi"> <a href=""><i class="fa-solid fa-bars"></i> More</a> 
              <ul>
                <li><a href="#">Servicio 1</a></li>
                <li><a href="#">Servicio 2</a></li>
                <li><a href="#">Servicio 3</a></li>
              </ul>
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

  