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
      friendID: null,
      show: true
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
            alert('Friend removed')
            window.location.reload()
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
    },
    async RedirectProfile(userID) {
      window.location.href = '/profile/' + userID
    },
    async goback(){
      window.history.back();
    },

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
        this.show = false
      }
      
      console.log(this.friendID+ " "+id)
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
      <a id="flechabackF" href="#" @click="goback()">
        <i class="fa-sharp fa-solid fa-arrow-left fa-2xl" style="color: #195583;" id="backArrow"></i>
      </a>
    </section>

    <!--Mostrar listas de deseos-->
    <section id="FriendsSection">
      <div id="banner">
        <h1>Amigos</h1>
      </div>
      <div id="FriendsElement">
        <ul id="ElementPartsF">
          <li v-for="llista in llistes" :key="llista.id">
            <div class="icon-container">
              <img id="profileImageJS" :src="llista.image" />
              <a @click="RedirectProfile(llista.id)"><h4>{{ llista.name }}</h4></a>
            </div>
            <div class="icon-container2" v-if="this.show">
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
    margin-top: 30% !important;
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
    margin-left: 215px;
  }
  #FriendsElement button {
    width: auto !important;
    font-size: 12px !important;
  }
  #FriendsElement img {
    width: 50px;
  }

  #ElementPartsF li {
    display: flex !important;
    margin-left: 0px !important;
    width: 225x !important;
  }

  #ElementPartsF::-webkit-scrollbar {
    width: 0px !important;
  }

  #flechabackF{
    margin-left: -375px;
    margin-top: -225px !important;
  }

  #ElementPartsF{
    width: 500px !important;
    padding-right: 0px !important; 
    height: 350px !important;
  }


  .upload-btn {
    margin-left: auto !important;
  }

  .popup-form button {
    margin-left: 30px !important;
  }

  #profileImageJS{
    width: 50px !important;
    height: 50px !important;
  }

  #backArrow{
    position: relative !important;
    top: 200px;
    left: 50px;
  }


}
</style>
