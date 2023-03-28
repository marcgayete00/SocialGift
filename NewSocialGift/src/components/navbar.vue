<template>
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
            <a href="createList"><i class="fa-solid fa-pen-to-square"></i> Create</a>
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
</template>

<style scoped>
@import "../assets/NavBar.css";
</style>
