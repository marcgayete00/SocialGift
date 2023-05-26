<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'


const token = localStorage.getItem('accessToken')


export default {
  name: 'MainView',
  components: {
    NavBar,
    language
  },
  data() {
    return {
      wishlists: [],
      gifts: [],
      listaId: null // Variable para almacenar el ID de la lista
    };
  },

  methods:{

    async addGift(){
      var url = document.getElementById('nombre-producto').value
      var prioridad = document.getElementById('prioridad-producto').value
      console.log(this.wishlists)
      const wishlist = {
        id: this.listaId,
        name: this.wishlists.name,
        description: this.wishlists.description,
        user_id: 121,
        gifts: [
          {
            id: 1,
            wishlist_id: this.listaId,
            product_url: url,
            priority: prioridad,
            booked: false
          }
        ],
      }
      console.log(wishlist)
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/wishlists/${this.listaId}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(wishlist)
      })
        .then((response) => {
          if (response.status === 200) {
            alert('Regalo añadido correctamente')
          } else {
            alert('Error al añadir el regalo')
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },

    async obtainGiftInfo() {

      const productURL = this.gifts.map((regalos) => regalos.product_url);

      //obtener el ultimo caracter de la URL despues de la ultima /
      const productIds = productURL.map((url) => url.substring(url.lastIndexOf('/') + 1));


      //hacer un flatMap para obtener un array de ids
      const flattenedProducIds = productIds.flatMap((obj) => obj)
      //hacer un fetch para cada URL
      const giftData = []
      for (let i = 0; i < flattenedProducIds.length; i++) {
        try {
          const response = await fetch(
            `https://balandrau.salle.url.edu/i3/mercadoexpress/api/v1/products/${flattenedProducIds[i]}`,
            {
              method: 'GET',
              headers: {
                'Content-Type': 'application/json'
              }
            }
          )
          if (response.status === 200) {
            const data = await response.json() // O response.text() si la respuesta es en formato de texto
            giftData.push(data)
          } else {
            throw new Error(`Failed to fetch gift for url ${product_urls[i]}.`)
          }
        } catch (error) {
          console.log(error)
        }
      }

      return giftData
    },

    async goback(){
      window.history.back();
    },

  },

  mounted() {
    this.listaId = this.$route.params.id; // Accede al ID de la lista desde la ruta
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
    //Hacer una peticion GET pasandole el email del usuario logueado
    fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/wishlists/${this.listaId}`, {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
          Authorization: `Bearer ${token}`
        }
      })
        .then((response) => {
          if (response.status === 200) {
            return response.json()
          }
        })
        .then(async (data) => {
          this.wishlists = data;
          console.log(this.wishlists);
          this.gifts = data.gifts;
          //mostrar el cotenido que nos devuelve el servidor
          document.getElementById('listanameJS').innerHTML = data.name
          document.getElementById('listadescJS').innerHTML = data.description
          
          const datagift = await this.obtainGiftInfo(); // Espera a que se resuelva la promesa
          this.gifts = datagift; // Asigna los datos obtenidos a this.gifts

        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
  }
}

</script>

<template>
  <div>
    <language />

    <section id="GeneralSection">
      <NavBar />
      <a id="flechaback" href="#" @click="goback()">
        <i class="fa-sharp fa-solid fa-arrow-left fa-2xl" style="color: #195583;"></i>
      </a>
    </section>

    

    <!--Mostrar listas de deseos-->
    <section id="WishListSection">
      <div id="banner">
        <h1 id="listanameJS"></h1>
        <h2 id="listadescJS"></h2>
      </div>
      <div v-if="gifts.length === 0">
        <h1>No hay regalos 😢</h1>
      </div>
      <div v-else  id="WishListElement">
        <ul id="ElementParts">
          <li v-for="gift in this.gifts" :key="gift.id">
            <div class="icon-container">
              <img :src="gift.photo">
              <a>{{ gift.name }}</a>
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
        <button id="close-button"><i class="fa-solid fa-xmark"></i></button>
        <h2>Añadir producto</h2>
        <label for="nombre-producto">Url del producto:</label>
        <input type="text" id="nombre-producto" name="nombre-producto">
        <label for="nombre-producto">Prioridad: </label>
        <input type="number" id="prioridad-producto" name="nombre-producto">

        <button @click="addGift()">Agregar</button>
      </form>
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
    margin-top: 20% !important;
    margin-left: 20px !important;
    height: 100% !important;
  }
  #banner h1{
    font-size: 20px !important;
  }

  #WishListElement{ 
    display: flex !important;
    margin-top: -50px;
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
    margin-top: -50px;
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
