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
      }
    }
  },

  methods: {
    async obtainFriendsWishlist(token, ids) {
      const wishlistData = []
      console.log(ids)
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
            wishlistData.push(data)
          } else {
            throw new Error(`Failed to fetch wishlist for user ${ids[i]}.`)
          }
        } catch (error) {
          console.error(error)
        }
      }
      console.log(wishlistData)
      return wishlistData
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
          //console.log(data) // debugging line
          this.friendList.friends = data
          const ids = data.map((obj) => obj.id)
          await this.obtainFriendsWishlist(token, ids)
        }
      } catch (error) {
        // Manejar el error de forma adecuada
      }
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
    }
  },
  mounted() {
    const token = localStorage.getItem('accessToken')
    console.log(token)
    if (token === undefined || token === null) {
      window.location.href = '/'
    } else {
      //llamar a la funcion que separa
      const id = MiComponente.methods.obtenerIdDesdeToken(token)

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

    <section id="GeneralSection">
      <NavBar />
      <div class="options-box">
        <div id="profile-box">
          <img id="profileImageJS" class="profileimg" src="" />
          <div>
            <h3><a id="usernameJS" href="profile"></a></h3>
            <h5 id="lastnameJS"><a></a></h5>
          </div>
        </div>
        <h3>Tus Listas</h3>
        <!--id 125-->
        <ul id="lista-nombres">
          <li v-if="llistes.length == 0">No tienes listas</li>
          <li v-for="llista in llistes">{{ llista.name }}</li>
        </ul>
        <h3>Plantillas de listas</h3>
        <ul>
          <li>💝 Lista de deseos</li>
          <li>🍰 Lista de cumpleaños</li>
          <li>🌓 Lista blanco y negro</li>
        </ul>
      </div>
      <div class="image-section">
        <div v-if="friendList.friends.length > 0">
          <div v-for="friend in friendList.friends" :key="friend.id">
            <div class="listheader">
              <img class="profileimglist" :src="friend.image" />
              <h3>{{ friend.name }}</h3>
              <img class="moreimg" src="../../img/Mas.png" />
            </div>
            <h1>My wishlist</h1>
            <h4>daadadadadadaddada</h4>
            <ul id="PostGiftList">
              <li class="product">
                <div class="emoji">🌓</div>
                <div class="name">Product name</div>
                <div class="checkbox"><input type="checkbox" id="reserveCheckbox" /></div>
              </li>
              <li class="product">
                <div class="emoji">🌓</div>
                <div class="name">Product name</div>
                <div class="checkbox"><input type="checkbox" id="reserveCheckbox" /></div>
              </li>
              <li class="product">
                <div class="emoji">🌓</div>
                <div class="name">Product name</div>
                <div class="checkbox"><input type="checkbox" id="reserveCheckbox" /></div>
              </li>
              <li class="product">
                <div class="emoji">🌓</div>
                <div class="name">Product name</div>
                <div class="Divcheckbox"><input type="checkbox" id="reserveCheckbox" /></div>
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
