<script setup>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
</script>
<template>
  <div>
    <language />

    <section id="GeneralSection">
      <NavBar />
    </section>

    <!--Mostrar listas de deseos-->
    <section id="WishListSection">
      <div id="banner">
        <h1>Amigos</h1>
      </div>
      <div id="WishListElement">
        <ul id="ElementParts">
          <li>
            <div class="icon-container">
              <img src="../../img/DefaultProfilePhoto.png">
              <a><h4>Martin50</h4></a>
            </div>
            <div class="icon-container2">
                <a href="#"><button id="EliminarButton">Eliminar</button></a>
            </div>
          </li>
          <li>
            <div class="icon-container">
                <img src="../../img/DefaultProfilePhoto.png">
                <a><h4>Patricia96</h4></a>
            </div>
            <div class="icon-container2">
                <a href="#"><button id="EliminarButton">Eliminar</button></a>
            </div>
          </li>
          <li>
            <div class="icon-container">
                <img src="../../img/DefaultProfilePhoto.png">
                <a><h4>Felixx</h4></a>
            </div>
            <div class="icon-container2">
                <a href="#"><button id="EliminarButton">Eliminar</button></a>
            </div>
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<style scoped>
@import '../assets/FriendsStyle.css';
</style>

<style>
@media screen and (max-width: 600px) {
  #WishListSection {
    margin-top: -175% !important;
    margin-left: 20px !important;
  }

  #WishListElement{ 
    display: flex !important;
    margin-left: -440px !important;

  }

  #ElementParts li{
    display: flex !important;
    margin-left: 0px !important;
    width: auto !important;
  }

  #ElementParts img{
    width: 60px;
  }

  #ElementParts h4{
    margin-left: 210px;
  }

  #EliminarButton{
    background-color: red;
    color: white;
    padding: 14px;
    font-size: 17px;
    border: white;
    font-weight: bold;
    border-radius: 7px;
  }
  
}
</style>
