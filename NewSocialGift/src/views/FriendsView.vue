<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
import MiComponente from './../components/separarTrama.vue'

export default {
  name: 'FriendsView',
  components: {
    NavBar,
    language,
    MiComponente
  },
  data() {
    return {
      llistes: [],
      friendID: null
    }
  },
  methods: {
    removeFriend(friendId) {
      const token = localStorage.getItem('accessToken')
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/friends/${friendId}`, {
        method: 'DELETE',
        headers: {
          Authorization: `Bearer ${token}`
        }
      })
        .then((response) => {
          if (response.status === 200) {
            ;-alert('Friend removed')
            window.location.replace('friends')
          } else {
            switch (response.status) {
              case 401:
                alert('Unauthorized')
                break

              case 500:
                alert('Error getting list of users friends')
                break

              default:
                alert('An error has occurred')
                break
            }
          }
        })
        .catch((error) => {
          // Respuesta en caso de error de servidor
        })
    }
  },
  mounted() {
    const token = localStorage.getItem('accessToken')
    console.log(token)

    if (token === null) {
      windows.location.href - '/'
    } else {
      //llamar a la funcion que separa
      const id = MiComponente.methods.obtenerIdDesdeToken(token)
      this.friendID = this.$route.params.id; // Accede al ID de la lista desde la ruta
      if(this.friendID != id){
        document.getElementById('EliminarButton').style.display = 'none'
      }
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${this.friendID}/friends`, {
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
          console.log(data)
          this.llistes = data
        })
        .catch((error) => {
          // Respuesta en caso de error de servidor
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
    </section>

    <!--Mostrar listas de deseos-->
    <section id="FriendsSection">
      <div id="banner">
        <h1>Amigos</h1>
      </div>
      <div id="FriendsElement">
        <ul id="ElementParts">
          <li v-for="llista in llistes" :key="llista.id">
            <div class="icon-container">
              <img id="profileImageJS" :src="llista.image" />
              <a
                ><h4>{{ llista.name }}</h4></a
              >
            </div>
            <div class="icon-container2">
              <a href="#" @click="removeFriend(llista.id)"><button id="EliminarButton">Eliminar</button></a>
            </div>
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<style scoped>
@import '../assets/FriendsStyle.css';
</style>

<style>
@media screen and (max-width: 600px) {
  #FriendsSection {
    margin-top: 20% !important;
    margin-left: 20px !important;
    height: 100% !important;
  }
  #banner h1 {
    font-size: 20px !important;
  }

  #FriendsElement {
    display: flex !important;
    margin-top: -50px;
    margin-left: -440px !important;
  }
  #FriendsElement h4 {
    font-size: 15px !important;
    width: 20px !important;
    margin-left: 225px;
  }
  #FriendsElement button {
    width: 75px;
    font-size: 12px !important;
  }
  #FriendsElement img {
    width: 50px;
  }

  #ElementParts li {
    display: flex !important;
    margin-left: 0px !important;
    width: auto !important;
  }

  /*Texto item*/
  .icon-container a {
    display: flex !important;
    margin-left: -220px !important;
    font-size: medium !important;
  }

  /*Iconos item*/
  .icon-container2 i {
    display: flex !important;
  }

  #share {
    position: relative !important;
    left: 15px !important;
    top: 2px !important;
  }

  #cross {
    position: relative !important;
    left: 15px !important;
    top: 2px !important;
  }

  .icon-container2 input {
    position: relative !important;
    left: 10px !important;
  }

  #addButton {
    display: flex !important;
    margin-top: -50px;
    margin-left: -650px !important;
  }

  #popup-container {
    display: hidden !important;
    left: 190px !important;
    top: 700px !important;
    width: 30% !important;
    height: 20% !important;
  }

  .upload-btn {
    margin-left: auto !important;
  }

  .popup-form button {
    margin-left: 30px !important;
  }
}
</style>
