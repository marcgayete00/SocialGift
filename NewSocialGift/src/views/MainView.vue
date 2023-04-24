<script setup>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
</script>

<script>
const token = localStorage.getItem('accessToken')
console.log(token)
</script>

<template>
  <div>
    <language />

    <section id="GeneralSection">
      <NavBar />
      <div class="options-box">
        <div id="profile-box">
          <img class="profileimg" src="../../img/DefaultProfilePhoto.png" />
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
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped src="../assets/mainStyle.css"></style>
<style>
@media screen and (max-width: 600px) {
  #GeneralSection {
    width: 100% !important;
    height: 100% !important;
  }
  .image-section {
    margin-top: 40px !important;
    width: 110% !important;
  }
  .options-box {
    visibility: hidden !important;
  }
  .listheader {
    width: 100% !important;
    height: 100px !important;
  }
  .listheader img {
    width: 60px !important;
  }
  .listheader h3 {
    margin-right: 150px !important;
  }
  .imageslide {
    width: 300px;
  }
}
</style>
