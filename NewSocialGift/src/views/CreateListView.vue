<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'

export default {
  name: 'MainView',
  components: {
    NavBar,
    language
  },

  methods:{
    async createWishlist() {
      const token = localStorage.getItem('accessToken')
      var nameInput = document.getElementById('listname').value;
      var descriptionInput = document.getElementById('listdesc').value;

   
      
      const wishlistData = {
        name: nameInput,
        description: descriptionInput,
        end_date: '2024-05-16T16:15:03.706Z'
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
        alert('Wishlist created successfully')
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
    }   
  }
}

</script>

<template>
    <language />

    <section id="GeneralSection">
      <NavBar v-bind:class="{ 'NavBar--show': showNavbar }"></NavBar>
    </section>

	<div class="container">
		<h1>Añadir lista</h1>
    <input type="text" class="inputRegister" id="listname" placeholder="Nombre de la lista" /><br />
    <input type="text" class="inputRegister" id="listdesc" placeholder="Descripción de la lista" /><br />
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