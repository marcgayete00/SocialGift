<script setup>
import language from './../components/language.vue'
</script>

<template>
      <language />
      
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
            <li id ="MoreLi">
              <a href="" onclick="openForm()"><i class="fa-solid fa-bars"></i> More</a>
            </li>
        </ul>
        </div>
        <section class="editarperfil-section">
            <h2 id="tituloeditarperf">Editar Perfil</h2>
            <div>
                <div id="headeditarperfil">
                    <img src="../../img/DefaultProfilePhoto.png">
                    <h2>NickName</h2>
                    <a href="#"><button id="EliminarButton">Eliminar Cuenta</button></a>
                </div>
                <a href="#"><h4>Cambiar Foto</h4></a>
                <div class="diveditarperfil">
                    <h3>Descripción</h3>
                    <textarea>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</textarea> 
                </div>
                <h5>12/100</h5>
                <div class="diveditarperfil">
                    <h3>Género</h3>
                    <select>
                        <option>Hombre</option>
                        <option>Mujer</option>
                        <option>Otro</option>
                    </select>
                </div>
                <div class="diveditarperfil">
                    <h3 id="titulocont">Cambiar Contraseña</h3>
                    <button>******</button>
                </div>
                <a href="#"><button id="GuardarButton">Guardar</button></a>
            </div>
        </section>
      </section>
  </template>

<style scoped>
@import '../assets/EditarPerfilStyle.css';
</style>
  