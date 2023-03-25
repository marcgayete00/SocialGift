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
              <input type="checkbox" id="reserveCheckbox">
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
              <input type="checkbox" id="reserveCheckbox">
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
              <input type="checkbox" id="reserveCheckbox">
            </div>
          </li>
        </ul>
      </div>

      <div id="addButton">
        <button><a href="#">Añadir</a></button>
      </div>

      <div id="popup-container">
      <form>
        <label for="nombre-producto">Nombre del producto:</label>
        <input type="text" id="nombre-producto" name="nombre-producto">
        <button type="submit">Agregar</button>
      </form>
    </div>

      <div id="saveButton">
        <button><a href="profile">Guardar</a></button>
      </div>
    </section>
  </div>
</template>
<style scoped>
@import '../assets/Wishlists.css';
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

  /*Texto item*/
  .icon-container a{
    display: flex !important;
    margin-left: -200px !important;
  }

  /*Iconos item*/
  .icon-container2 i{
    display: flex !important;
    margin-left: -90px !important;
  }

  .icon-container2 input{
    margin-left: -30px !important;
  }
  

  
}
</style>
