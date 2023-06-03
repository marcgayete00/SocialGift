<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
import MiComponente from './../components/separarTrama.vue'

export default {
  name: 'MainView',
  components: {
    NavBar,
    language
  },
  data() {
    return {
      llistes: [],
      friendList: {
        friends: []
      },
      mainId: null // Variable para almacenar el ID
    }
  },

  methods: {
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

    async obtainGiftInfo(wishlists) {
      const gifts = wishlists.map((obj) => obj.gifts)
      //console.log(gifts)

      const productURL = wishlists.map((wishlist) => {
        return wishlist.gifts.map((gift) => gift.product_url)
      })
      //console.log(productURL)
      //obtener el ultimo caracter de la URL despues de la ultima /
      const productIds = productURL.map((url) => {
        return url.map((url) => url.substring(url.lastIndexOf('/') + 1))
      })
      //console.log(productIds)

      //hacer un flatMap para obtener un array de ids
      const flattenedProducIds = productIds.flatMap((obj) => obj)
      //hacer un fetch para cada URL
      //console.log(flattenedProducIds)
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
      //console.log(giftData)

      gifts.forEach((element) => {
        const productIds = element.map((gift) => {
          const id = gift.product_url.substring(gift.product_url.lastIndexOf('/') + 1)
          giftData.forEach((giftDataElement) => {
            if (giftDataElement.id == id) {
              // copiar los campos name y description del array giftData al array gifts
              gift.name = giftDataElement.name
              gift.description = giftDataElement.description
              gift.link = giftDataElement.link
              gift.photo = giftDataElement.photo
              gift.categoryIds = giftDataElement.categoryIds
            }
          })
        })
      })

      return gifts
    },

    async obtainFriendsWishlist(token, ids) {
      const wishlistData = []
      //console.log(ids)
      for (let i = 0; i < ids.length; i++) {
        try {
          const response = await fetch(
            `https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${ids[i]}/wishlists`,
            {
              method: 'GET',
              headers: {
                Authorization: `Bearer ${token}`
              }
            }
          )
          if (response.status === 200) {
            const data = await response.json() // O response.text() si la respuesta es en formato de texto
            const currentDate = new Date().toISOString();
            let notExpired = [];
            for(let j = 0; j < data.length; j++){
              if (data[j].end_date > currentDate){
                notExpired.push(data[j])
              } else {
                console.log("Lista caducada "+ data[j].name)
              }
            }
           
            for(let j = 0; j < notExpired.length; j++){
             console.log(notExpired[j].name)
            }

            wishlistData.push(notExpired)


          } else {
            throw new Error(`Failed to fetch wishlist for user ${ids[i]}.`)
          }
        } catch (error) {
          console.error(error)
        }
      }
      const flattenedArray = wishlistData.flatMap((obj) =>
        obj.map((item) => ({
          id: item.id,
          user_id: item.user_id,
          name: item.name,
          description: item.description,
          creation_date: item.creation_date,
          end_date: item.end_date,
          gifts: item.gifts
        }))
      )
      

      return flattenedArray
    },

    async obtainFriends(token, id) {
      try {
        const response = await fetch(
          `https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${id}/friends`,
          {
            method: 'GET',
            headers: {
              Authorization: `Bearer ${token}`
            }
          }
        )
        if (response.status === 200) {
          const data = await response.json()
          //console.log(data) // Show friends

          const ids = data.map((obj) => obj.id)
          const wishlists = await this.obtainFriendsWishlist(token, ids)
          //console.log(wishlists)
          const gifts = await this.obtainGiftInfo(wishlists)
          //console.log(wishlists)
          //console.log(gifts)
          //Hacer un flatMa para obtener un array de gifts
          const flattenedGifts = gifts.flatMap((obj) => obj)
          //console.log(flattenedGifts)

          // Itera sobre el array wishlists y busca el amigo correspondiente en friends
          data.forEach((friend) => {
            friend.wishlists = wishlists.filter((list) => list.user_id === friend.id)
          })

          //Iterar sobre el array data y añadir los gifts correspondientes a cada wishlist
          data.forEach((friend) => {
            friend.wishlists.forEach((wishlist) => {
              wishlist.gifts = flattenedGifts.filter((gift) => gift.wishlist_id === wishlist.id)
            })
          })
          //console.log(data)
          this.friendList.friends = data //Array al que queremos meter los regalos
          console.log("Friends"+ this.friendList.friends.length)
        }
      } catch (error) {
        // Manejar el error de forma adecuada
      }
    },

    async Redirectllista(llistaID) {
      window.location.href = '/wishlist/' + llistaID
    },

    async RedirectProfile(profileID) {
      window.location.href = '/profile/' + profileID
    },

    async obtainOwnWishlist(token, id) {
      try {
        const response = await fetch(
          `https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${id}/wishlists`,
          {
            method: 'GET',
            headers: {
              Authorization: `Bearer ${token}`
            }
          }
        )
        if (response.status === 200) {
          const data = await response.json()
          //console.log("Listas usuario actual ")
          //console.log(data)
          this.llistes = data
          await this.obtainFriends(token, id)
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
  },
  mounted() {
    
    const token = localStorage.getItem('accessToken')
    //console.log(token)
    if (token === undefined || token === null) {
      window.location.href = '/'
    } else {
      //llamar a la funcion que separa
      const id = MiComponente.methods.obtenerIdDesdeToken(token)
      this.mainId = id
      //Hacer una peticion GET pasandole el email del usuario logueado
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${id}`, {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
        .then((response) => {
          if (response.status === 200) {
            return response.json()
          }
        })
        .then((data) => {
          //mostrar el cotenido que nos devuelve el servidor
          document.getElementById('usernameJS').innerHTML = data.name
          document.getElementById('lastnameJS').innerHTML = data.last_name
          document.getElementById('profileImageJS').src = data.image
          this.obtainOwnWishlist(token, id) // aquí agregamos el operador this
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
    }
  }
}
</script>

<template>
  <div>
    <language />
   <a @click="toggleTaskBar()" class="togleNavBar" ><i class="fa-solid fa-bars"></i></a>
    <section id="MainGeneralSection">
      <NavBar />
      <div class="options-box">
        <div id="profile-box">
          <img id="profileImageJS" class="profileimg" src="" />
          <div>
            <h3><a id="usernameJS" @click="RedirectProfile(this.mainId)"></a></h3>
            <h5 id="lastnameJS"><a></a></h5>
          </div>
        </div>
        <h3>Tus Listas</h3>
        <!--id 125-->
        <ul id="lista-nombres">
          <li v-if="llistes.length == 0">No tienes listas</li>
          <li v-for="llista in llistes" key:llista.id><a id="tulista" @click="Redirectllista(llista.id)">{{ llista.name }}</a></li>
        </ul>
        <h3>Plantillas de listas</h3>
        <ul>
          <li><a href="createlist">💝 Lista de deseos</a></li>
          <li><a href="createlist">🍰 Lista de cumpleaños</a></li>
          <li><a href="createlist">🌓 Lista blanco y negro</a></li>
        </ul>
      </div>
      <div class="image-section">
      <div v-if="this.friendList.friends.length === 0">
        <h1>No hay listas de deseos disponibles 😢</h1>
        <h2 style="font-weight: normal;">¡Agrega a mas amigos!</h2>
      </div>
      <div v-for="friend in friendList.friends" :key="friend.id">
        <!-- Mostrar un mensaje en caso de no tener wishlists-->
          <div id="listamigo" v-for="wishlist in friend.wishlists" :key="wishlist.id">
            <div class="listheader">
              <img class="profileimglist" :src="friend.image" />
              <h3 @click="RedirectProfile(friend.id)">{{ friend.name }}</h3>
            </div>

            <h1 @click="Redirectllista(wishlist.id)">{{ wishlist.name }}</h1>
            <h4>{{ wishlist.description }}</h4>
            <ul id="PostGiftList">
              <li class="product" v-for="gift in wishlist.gifts" :key="gift.id">
                <div class="emoji"><img id="giftImage" :src="gift.photo" /></div>
                <div class="name">{{ gift.name }}</div>
                <div class="checkbox"><input type="checkbox" id="reserveCheckbox" :checked="gift.booked" v-on:click="bookGift(gift.id, gift.booked)" /></div>
              </li>
            </ul>
          
        </div>
      </div>
       
</div>

    </section>
  </div>
</template>

<style scoped src="../assets/mainStyle.css"></style>
<style>
@media screen and (max-width: 600px) {
  #MainGeneralSection {
    width: 100% !important;
    height: 100% !important;
    margin-top: -30px !important;
  }
  .image-section {
    margin-top: 40px !important;
    width: 110% !important;
  }

  .options-box{
    display: none;
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

  .togleNavBar{
    position: fixed !important;
    display: block !important;
    font-size: 35px !important;
    margin-left: 300px;
    margin-top: -70px;
  }
}
</style>
