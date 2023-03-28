<script setup>
import language from './../components/language.vue'
import NavBar from './../components/NavBar.vue'
</script>

<template>
    <language />

    <section id="GeneralSection">
      <NavBar v-bind:class="{ 'NavBar--show': showNavbar }"></NavBar>
    </section>

	<div class="container">
		<h1>Añadir lista</h1>
		<input type="text" placeholder="Nombre de la lista">
        <label class="colorPickerLabel"> Color: </label>
        <input type="color" class="colorPicker" value="#79B2DD"><br>
		<input type="submit" value="Enviar">
	</div>    
</template>

<script>
export default {
  mounted() {
    // Esperar a que el DOM se cargue antes de seleccionar el botón
    var button = document.getElementById("color-button");
    button.onclick = function() {
      // Crear un elemento de entrada de color
      var colorPicker = document.createElement("input");
      colorPicker.type = "color";

      // Agregar un evento de cambio de color
      colorPicker.onchange = function() {
        button.style.backgroundColor = colorPicker.value;
      };

      // Mostrar el selector de color
      colorPicker.click();
    };
  }
}
</script>
<style scoped>
@import '../assets/CreateList.css';
</style>

<style>
    @media screen and (max-width: 600px) {
        .container {
            width: 80% !important;
            height: auto !important;
        }
    }
</style>