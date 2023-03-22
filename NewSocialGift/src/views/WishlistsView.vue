<script setup>
  import NavBar from './../components/NavBar.vue'
</script>
<template>
  <div>
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
      <NavBar/>
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
        <button><a>Añadir</a></button>
      </div>

      <div id="saveButton">
        <button><a>Guardar</a></button>
      </div>
    </section>
  </div>
</template>
<style scoped>
@import "../assets/ProfileStyle.css";
@import "../assets/Wishlists.css";
</style>
