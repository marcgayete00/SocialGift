<script setup>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
</script>

<template>
    <div>
    <language/>

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
            <h3>Amigos</h3>
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
        <div class="grid-item" onclick="myFunction()">1</div>
        <div class="grid-item" onclick="myFunction()">2</div>
        <div class="grid-item" onclick="myFunction()">3</div>
        <div class="grid-item" onclick="myFunction()">4</div>
        <div class="grid-item" onclick="myFunction()">5</div>
        <div class="grid-item" onclick="myFunction()">6</div>
      </div>
    </section>
  </div>
</template>
<style>
  @media screen and (max-width: 600px) {
    #ProfileSection{
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: -50%;
    }


    .navigation{
      display: none;
    }
  }
</style>

<style scoped src="../assets/ProfileStyle.css"></style>
