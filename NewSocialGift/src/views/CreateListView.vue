<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
import MiComponente from './../components/separarTrama.vue'

export default {
  name: 'MainView',
  components: {
    NavBar,
    language,
    MiComponente
  },

  methods:{

    async RedirectUser(id) {
      console.log(id)
      window.location.href = '/profile/' + id
    },

    async createWishlist() {
      const token = localStorage.getItem('accessToken')
      var nameInput = document.getElementById('listname').value;
      var descriptionInput = document.getElementById('listdesc').value;
      var dateInput = document.getElementById('listdate').value;

      // Convertir la fecha de entrada a un objeto Date
      var date = new Date(dateInput);
      
      // Obtener los componentes de fecha necesarios
      var year = date.getFullYear();
      var month = String(date.getMonth() + 1).padStart(2, '0');
      var day = String(date.getDate()).padStart(2, '0');
      var hours = String(date.getHours()).padStart(2, '0');
      var minutes = String(date.getMinutes()).padStart(2, '0');
      var seconds = String(date.getSeconds()).padStart(2, '0');
      
      // Crear la cadena de fecha en el formato deseado
      var formattedDate = `${year}-${month}-${day}T${hours}:${minutes}:${seconds}.000Z`;

   
      const wishlistData = {
        name: nameInput,
        description: descriptionInput,
        end_date: formattedDate
      };
      try {
        console.log(wishlistData)
        const response = await fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/wishlists`,
          {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
              Authorization: `Bearer ${token}`
            },
            body: JSON.stringify(wishlistData)
          }
        )
        if (response.status === 201) {
        alert('Wishlist created successfully');
        const id = MiComponente.methods.obtenerIdDesdeToken(token)
        this.RedirectUser(id)
        return response.json()
        } else {
          switch (response.status) {
            case 400:
              alert('An error has occurred')
              break
            case 406:
              alert('Missing parameters')
              break
            case 409:
              alert('The wish list has already been pre-registered')
              break
            case 500:
              alert('The wish list has not been created')
              break
            case 502:
              alert('Internal Server Error')
              break
          }
        }
            
            
      } catch (error) {
        // Manejar el error de forma adecuada
      }    
    },
    toggleTaskBar(){
      const navigation = document.querySelector('.navigation');
      if (navigation) {
        navigation.style.display = 'block';
      }
    }   
  }
}

</script>

<template>
    <language />
    <a @click="toggleTaskBar()" class="togleNavBar" ><i class="fa-solid fa-bars"></i></a>
    <section id="GeneralSection">
      <NavBar v-bind:class="{ 'NavBar--show': showNavbar }"></NavBar>
    </section>

	<div class="container">
		<h1>Añadir lista</h1>
    <input type="text" class="inputRegister" id="listname" placeholder="Nombre de la lista" /><br />
    <input type="text" class="inputRegister" id="listdesc" placeholder="Descripción de la lista" /><br />
    <input type="date" class="inputRegister" id="listdate" placeholder="Fecha de caducidad" /><br />
    <button type="submit" @click="createWishlist">Enviar</button>

	</div>    
</template>

<style scoped>
@import '../assets/CreateList.css';
</style>

<style>
    @media screen and (max-width: 600px) {
        .container {
            margin-top: 75px !important;
            width: 80% !important;
            height: auto !important;
        }
    }
</style>