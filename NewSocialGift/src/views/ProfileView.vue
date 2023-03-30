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

    <!--Mostrar perfil-->
    <section id="ProfileSection">
      <div>
        <div>
          <button id="EditProfileButton"><a href="editarperfil">Editar perfil</a></button>
        </div>
        <div id="ProfileInfo">
          <div id="ProfileImage">
            <img src="img/DefaultProfilePhoto.png" />
            
          </div>
          <div id="ProfileName">
            <h1>Pablo03</h1>
          </div>
          <div id="UserCount">
            <h1>6</h1>
            <h3>Listas</h3>
            <h1>340</h1>
            <a href="friends"><h3>Amigos</h3></a>
          </div>
          <div id="ProfileDescription">
            <p>
              Lorem Ipsum is simply dummy text of the printing and typesetting industry. del usuario
            </p>
          </div>
        </div>
      </div>
    </section>
    <hr />

    <section>
      <div id="SelectList">
        <a href="#" id="Lists">List</a>
        <a href="#" id="Lists">WishList</a>
      </div>
    </section>
    <section id="PostSection">
      <div class="grid-container">
        <div class="grid-item" @click="myFunction()">1</div>
        <div class="grid-item" @click="myFunction()">2</div>
        <div class="grid-item" @click="myFunction()">3</div>
        <div class="grid-item" @click="myFunction()">4</div>
        <div class="grid-item" @click="myFunction()">5</div>
        <div class="grid-item" @click="myFunction()">6</div>
        <div class="grid-item" @click="myFunction()">7</div>
        <div class="grid-item" @click="myFunction()">8</div>
        <div class="grid-item" @click="myFunction()">9</div>
        <div class="grid-item" @click="myFunction()">10</div>
        <div class="grid-item" @click="myFunction()">11</div>
        <div class="grid-item" @click="myFunction()">12</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  methods: {
    myFunction() {
      window.location.href = '/Wishlists';
    }
  }
}
</script>

<style>
  @media screen and (max-width: 600px) {
    #ProfileSection{
      margin-top: -190% !important;
    }

    #EditProfileButton{
      position: relative !important;
      margin-left: 73% !important;
      top: 50px !important;
      font-size: medium !important;
      width: auto !important;
      height: 30px !important;
    }

    .navigation{
      display: none;
    }

    #GeneralSection{
      margin-top: -10% !important;
    }

    hr{
      width: auto !important;
    }

    #SelectList a{
      font-family: 'Inter', sans-serif;
    }

    .grid-container {
      display: grid;
      margin-left: 4% !important;
      grid-template-columns: repeat(3, 1fr) !important;
      grid-template-rows: repeat(2, 1fr) !important;
      gap: 50px !important;
      width: 80vw; /* Ajusta el ancho del contenedor a la ventana */
      height: 10vh !important; /* Ajusta la altura del contenedor a la ventana */
    }
    

    .grid-item{
      height: 90% !important;
      width: 90% !important;

      
      
    }
  }
</style>

<style scoped src="../assets/ProfileStyle.css"></style>
