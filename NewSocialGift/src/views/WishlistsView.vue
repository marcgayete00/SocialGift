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
              <a href="main"> <img src="../../img/logo.png" id="logoNavBar" alt="" /></a>
            </li>
            <li>
              <a href="main"><i class="fa-solid fa-house"></i> Home</a>
            </li>
            <li>
              <a href="#"><i class="fa-solid fa-magnifying-glass"></i> Search</a>
              <ul id="SearchSlide">
                <li>
                  <input type="text" placeholder="Search..."/>
                  <i class="fa-solid fa-user"><a href="#">Martin50</a></i>
                  
                </li>
              </ul>
            </li>
            <li>
              <a href="chat"><i class="fa-solid fa-envelope"></i> Messages</a>
            </li>
            <li>
              <a href="#"><i class="fa-sharp fa-solid fa-bell"></i> Notifications</a>
              <ul id="NotificationsSlide">
                <li style="font-size: larger;">Más recientes</li>
                <li id="InsideNotificationSlide">
                  <i class="fa-solid fa-user"></i>
                  <a>Patricia96</a>
                  <p>Te ha empezado a seguir</p>
                  <button>Seguir</button>
                </li>
              </ul>
            </li>
            <li>
              <a href=""><i class="fa-solid fa-pen-to-square"></i> Create</a>
            </li>
            <li id="MoreLi">
              <a href="#"><i class="fa-solid fa-bars"></i> More</a>
              <ul id="moreSlide">
                <li><a href="editarperfil">Editar Perfil</a></li>
                <li><a href="/">Desconectar</a></li>
              </ul>
            </li>
          </ul>
        </div>
      </section>
  
      <!--Mostrar listas de deseos-->
      <section id="WishListSection">
       <div id="banner">
        <h1>Lista de cumpleaños</h1>
       </div>
            <div id="WishListElement">
                <ul id="ElementParts">
                    <li>
                        <div class="icon-container">
                            <i class="fa-brands fa-playstation"></i>
                            <a>PlayStation 5</a>
                        </div>
                        <div class="icon-container2">
                            <a><i class="fa-solid fa-share-from-square"></i></a>
                            <a><i id="cross" class="fa-solid fa-circle-xmark"></i></a>
                        </div>
                    </li>
                    <li>
                        <div class="icon-container">
                            <i class="fa-brands fa-xbox"></i>
                            <a>Xbox one</a>
                        </div>
                        <div class="icon-container2">
                            <a><i class="fa-solid fa-share-from-square"></i></a>
                            <a><i id="cross" class="fa-solid fa-circle-xmark"></i></a>
                        </div>
                    </li>
                    <li>
                        <div class="icon-container">
                            <i class="fa-solid fa-desktop"></i>
                            <a>Desktop computer</a>
                        </div>
                        <div class="icon-container2">
                            <a><i class="fa-solid fa-share-from-square"></i></a>
                            <a><i id="cross" class="fa-solid fa-circle-xmark"></i></a>
                        </div>
                    </li>
                </ul>
            </div>

            <div id="addButton">
                <button ><a>Añadir</a></button>
            </div>

            <div id="saveButton">
                <button ><a>Guardar</a></button>
            </div>
            
       
       
      </section>


    </body>
  </template>
  <style scoped src="../assets/ProfileStyle.css"></style>
  <style scoped src="../assets/Wishlists.css"></style>
  