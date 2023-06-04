<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
import MiComponente from './../components/separarTrama.vue'
import gift from './../components/gift.vue'


const token = localStorage.getItem('accessToken')


export default {
  name: 'MainView',
  components: {
    gift,
    NavBar,
    language,
    MiComponente
  },
  data() {
    return {
      wishlists: [],
      gifts: [],
      listaId: null, // Variable para almacenar el ID de la lista
      mainId: null,
      show: false,
      llistes: [],
      gifttoShare: null
    };
  },

  methods:{

    async addGift() {
      var url = document.getElementById('nombre-producto').value;
      var prioridad = document.getElementById('prioridad-producto').value;

      const giftData = {
        wishlist_id: this.listaId,
        product_url: url,
        priority: prioridad
      };

      try {
        const response = await fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/gifts', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token}`
          },
          body: JSON.stringify(giftData)
        });

        if (response.status === 200) {
          alert('Regalo añadido correctamente');
        } else {
          alert('Error al añadir el regalo');
        }
      } catch (error) {
        console.log(error);
      }
    },

    async obtainGiftInfo() {
      //obtener el array de product_urls
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

    async ComprobarLista(){
      try {
        const response = await fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${this.mainId}/wishlists`, {
          method: 'GET',
          headers: {
            Authorization: `Bearer ${token}`
          }
        });
        if (response.status === 200) {
          const data = await response.json();
          this.llistes = data;
          for(let i = 0; i < this.llistes.length; i++){
            if(this.llistes[i].id == this.listaId){
              this.show = true;
              return;
            }else{
              this.show = false;
            }
          }

        }
      } catch (error) {
        // Manejar el error de forma adecuada
      }
      console.log(this.show)

    },

    async RemoveGift(giftId){
      console.log(giftId)
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/gifts/${giftId}`, {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json',
          Authorization: `Bearer ${token}`

        }
      })
        .then((response) => {
          if (response.status === 200) {
            alert('Regalo eliminado correctamente')
            window.location.reload()
          } else {
            alert('Error al eliminar el regalo')
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },

    async RemoveList(){
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/wishlists/${this.listaId}`, {
        method: 'DELETE',
        headers: {
          'Content-Type': 'application/json',
          Authorization: `Bearer ${token}`
        }
      })
        .then((response) => {
          if (response.status === 200) {
            alert('Lista eliminada correctamente')
            window.history.back();
          } else {
            alert('Error al eliminar la lista')
          }
        })
        .catch((error) => {
          console.log(error)
        })
    },

    async bookGift(id, booked){
        let toBook = false;
        let method = 'POST';
        const token = localStorage.getItem('accessToken')
        if (!booked){
          toBook = true;
        } else {
          method = 'DELETE';
        }
        
        //Hacer un post para indicar que el book de un regalo ha sido cambiado
        try {
          const response = await fetch(
            `https://balandrau.salle.url.edu/i3/socialgift/api/v1/gifts/${id}/book`,
            {
              method: method,
              headers: {
                'Content-Type': 'application/json',
                Authorization: `Bearer ${token}`
              },
            }
          )
          if (response.status === 200) {
            const data = await response.json()
          } else {

          } 
          
        } catch (error) {
          // Manejar el error de forma adecuada
        }

      },
    async MoveGift(wishlistID) {

      const moveData = {
        wishlist_id: wishlistID
      }

      try {
        const response = await fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/gifts/${this.gifttoShare}`, {
          method: 'PUT',
          headers: {
            'Content-Type': 'application/json',
            Authorization: `Bearer ${token}`
          },
          body: JSON.stringify(moveData)
        });

        if (response.status === 200) {
          alert('Regalo movido correctamente');
        } else {
          alert('Error al mover el regalo');
        }
      } catch (error) {
        console.log(error);
      }
      window.location.reload()
    },

    async closeP2(){
      const popupContainer2 = document.querySelector('#popup-container2');
      const popupOverlay = document.querySelector('#popup-overlay');
      popupContainer2.classList.remove('show-popup');
      popupOverlay.style.display = 'none';
    },
    
    async showPopup2(giftID){
      this.gifttoShare = giftID;
      const popupContainer2 = document.querySelector('#popup-container2');
      const popupOverlay = document.querySelector('#popup-overlay');
      popupContainer2.classList.add('show-popup');
      popupOverlay.style.display = 'block';
    },
    toggleTaskBar(){
      const navigation = document.querySelector('.navigation');
      if (navigation) {
        navigation.style.display = 'block';
      }
    } 
  },

  mounted() {
    this.listaId = this.$route.params.id; // Accede al ID de la lista desde la ruta
    const id = MiComponente.methods.obtenerIdDesdeToken(token)
    this.mainId = id; // Accede al ID de la lista desde la ruta
    const addButton = document.querySelector('#addButton');

    const popupContainer = document.querySelector('#popup-container');
    const popupOverlay = document.querySelector('#popup-overlay');

    if(addButton != null){
      addButton.addEventListener('click', function() {
        popupContainer.classList.add('show-popup');
        popupOverlay.style.display = 'block';
      });
    }
    popupContainer.addEventListener('click', function(event) {
      if (event.target === popupContainer) {
        popupContainer.classList.remove('show-popup');
        popupOverlay.style.display = 'none';
      }
    });
    this.ComprobarLista();

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
          console.log(this.wishlists)
          this.gifts = data.gifts;
          const fecha = data.end_date;
          const fechaObjeto = new Date(fecha);

          const fechaFormateada = fechaObjeto.toISOString().split('T')[0];
          const currentDate = new Date().toISOString().split('T')[0];
          const listadateElement = document.getElementById('listadateJS');
          listadateElement.innerHTML = fechaFormateada;

          if (fechaFormateada < currentDate) {
            listadateElement.style.color = 'red';
          } else {
            listadateElement.style.color = 'green';
          }

          //mostrar el cotenido que nos devuelve el servidor
          document.getElementById('listanameJS').innerHTML = data.name
          document.getElementById('listadescJS').innerHTML = data.description
          // Asigna los datos obtenidos a this.gifts
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
    <a @click="toggleTaskBar()" class="togleNavBar" ><i class="fa-solid fa-bars"></i></a>
    <section id="GeneralSection">
      <NavBar />
      <a id="flechaback" href="#" @click="goback()">
        <i class="fa-sharp fa-solid fa-arrow-left fa-2xl" style="color: #195583;"></i>
      </a>
    </section>

    

    <!--Mostrar listas de deseos-->
    <section id="WishListSection">
      <div id="banner">
        <button v-if="this.show" id="RemoveButton" @click="RemoveList()">Eliminar Lista</button>
        <h1 id="listanameJS"></h1>
        <h2 id="listadescJS"></h2>
        <h2 id="listadateJS"></h2>
      </div>
      <div v-if="gifts.length === 0">
        <h1 id="NoRegalos">No hay regalos 😢</h1>
      </div>
      <div v-else  id="WishListElement">
        <ul id="ElementParts">
          <li v-for="gift in this.gifts" :key="gift.id">
            <gift :gift="gift"/>
            <div class="icon-container2" v-if="this.show">
              <a @click="showPopup2(gift.id)"><i id="share" class="fa-solid fa-share-from-square"></i></a>
              <a @click="RemoveGift(gift.id)"><i id="cross" class="fa-solid fa-circle-xmark"></i></a>
            </div>
            <div class="checkbox"><input type="checkbox" id="reserveCheckbox" :checked="gift.booked" @click="bookGift(gift.id, gift.booked)" /></div>

          </li>
        </ul>
      </div>

      <div id="addButton">
        <button v-if="this.show"><a href="#">Añadir</a></button>
      </div>


      <div id="popup-overlay"></div>
      <div id="popup-container2">
          <button @click="closeP2()" id="close-button"><i class="fa-solid fa-xmark"></i></button>
          <h2>Elige una Wishlist</h2>
          <ul v-for="lista in this.llistes" :key="lista.id">
            <li @click="MoveGift(lista.id)">{{ lista.name }}</li>
          </ul>
      </div>
      <div id="popup-container">
        <form class="popup-form">
          <button id="close-button"><i class="fa-solid fa-xmark"></i></button>
          <h2>Añadir producto</h2>
          <label for="nombre-producto">Url del producto:</label>
          <input type="text" id="nombre-producto" name="nombre-producto">
          <label for="prioridad-producto">Prioridad: </label>
          <input type="number" id="prioridad-producto" name="prioridad-producto">
          <!--<label for="fecha-caducidad">Fecha de caducidad: </label>
          <input type="date" id="fecha-caducidad" name="fecha-caducidad">-->
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
    margin-top: 10% !important;
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

  #ElementParts{
    width: 500px !important;
    padding-right: 0px !important; 
    height: 350px !important;
  }

  #ElementParts::-webkit-scrollbar {
    width: 0em !important;
  }

  #ElementParts li{
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px !important;
      width: 280px !important;
      margin-left: 40px;
      height: 60px !important;
      padding: 0px !important;
  }

  #ElementParts i{
      font-size:xx-large;
  }

  #ElementParts a{
    font-size: x-large;
    color: #000;
  }

  #ElementParts .namegift{
    font-size: 15px !important;
    margin-left: -190px !important;
  }

  #ElementParts .imggift{
    width: 60px !important;
    height: 40px !important;
  }

  #flechaback{
    margin-left: -275px !important;
    margin-top: 60px !important;
  }

  /*Texto item*/
  .icon-container a{
    display: flex !important;
    margin-left: -220px !important;
    font-size:medium !important;
  }

  .icon-container2 {
    margin-left: 0px !important;
  }

  .icon-container2 a{
    margin-left:2px !important;
    margin-right: 5px;
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

  #addButton {
    display: flex !important;
    margin-top: -50px;
    margin-left: -650px !important;
  }

  #addButton button{
    width: 120px !important;
    font-size: 15px !important;
    margin-top: -48px !important;
    margin-left: 795px !important;
    position: fixed !important;
  }

  #RemoveButton{
    width: 120px !important;
    font-size: 15px !important;
    margin-left: 0px !important;
    margin-top: 550px;
    position: fixed !important;
  }
  

  #popup-container{
    display: hidden !important;
    width: 300px !important;  
  }

  .upload-btn{
    margin-left: auto !important;
  }

  .popup-form button{
    margin-left: 30px !important;
  }

  
}
</style>
