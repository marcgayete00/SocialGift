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
              <a><i id="share" class="fa-solid fa-share-from-square"></i></a>
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
              <a><i id="share" class="fa-solid fa-share-from-square"></i></a>
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
              <a><i id="share" class="fa-solid fa-share-from-square"></i></a>
              <a><i id="cross" class="fa-solid fa-circle-xmark"></i></a>
              <input type="checkbox" id="reserveCheckbox">
            </div>
          </li>
        </ul>
      </div>

      <div id="addButton">
        <button><a href="#">Añadir</a></button>
      </div>

      <div id="popup-overlay"></div>
      <div id="popup-container">
      <form class="popup-form">
        <h2>Añadir producto</h2>
        <label for="nombre-producto">Nombre del producto:</label>
        <input type="text" id="nombre-producto" name="nombre-producto">
        <label for="file-upload" class="upload-btn">Imagen del producto:</label>
        <input type="file" id="file-upload">
        <button type="submit">Agregar</button>
      </form>
    </div>

      <div id="saveButton">
        <button><a href="profile">Guardar</a></button>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  mounted() {
    const addButton = document.querySelector('#addButton button');
    const popupContainer = document.querySelector('#popup-container');
    const popupOverlay = document.querySelector('#popup-overlay');

    addButton.addEventListener('click', function() {
      popupContainer.classList.add('show-popup');
      popupOverlay.style.display = 'block';
    });

    popupContainer.addEventListener('click', function(event) {
      if (event.target === popupContainer) {
        popupContainer.classList.remove('show-popup');
        popupOverlay.style.display = 'none';
      }
    });

  }
}
</script>

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
    margin-left: -220px !important;
    font-size:medium !important;
   
  }

  /*Iconos item*/
  .icon-container2 i{
    display: flex !important;
  }

  #share{
    position: relative !important;
    left: 15px !important;
    top: 2px !important;
  }

  #cross{
    position: relative !important;
    left: 15px !important;
    top: 2px !important;
  }

  .icon-container2 input{
    position: relative !important;
    left: 10px !important;
  }

  #addButton{
    display: flex !important;
    margin-left: -650px !important;
  }

  #popup-container{
    display: hidden !important;
    left: 190px !important;
    top: 700px !important;
    width: 30% !important;  
    height: 20% !important;
  }

  .upload-btn{
    margin-left: auto !important;
  }

  .popup-form button{
    margin-left: 30px !important;
  }

  
}
</style>
