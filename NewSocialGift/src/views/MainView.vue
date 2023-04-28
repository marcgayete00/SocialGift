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
      llistes: []
    }
  },
  methods: {
    
    obtainFriendsWishlist(token,ids) {
      let wishlists = [];
      for(let i = 0; i < ids.length; i++) {
            fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${ids[i]}/wishlists`, {

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
                console.log(ids[i])
                console.log(data)
                wishlists.push = data
                
              })
              .catch((error) => {
                // Respuesta en caso de error de servidor
              })
          }
          console.log(wishlists)
    },

    obtainFriends(token, id){
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${id}/friends`, {
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
          //console.log("Amigos usuario actual ")
          //console.log(data)
          const ids = data.map(obj => obj.id);
          this.obtainFriendsWishlist(token,ids)
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
    },
    
    obtainOwnWishlist(token,id){

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/${id}/wishlists`, {
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
          //console.log("Listas usuario actual ")
          //console.log(data)
          this.llistes = data
          this.obtainFriends(token, id)
        })
        .catch((error) => {
          // Respuesta en caso de error de servidor
        })
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
          <li v-if = "llistes.length == 0">No tienes listas</li>
          <li v-for="llista in llistes">{{ llista.name }}</li>
          
        </ul>
        <h3>Plantillas de listas</h3>
        <ul>
          <li>Lista de deseos</li>
          <li>Lista de cumpleaños</li>
          <li>Lista blanco y negro</li>
        </ul>
      </div>
      <div class="image-section">
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
        </div>
        <div>
          <div class="listheader">
            <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" />
            <h3>NickName</h3>
            <img class="moreimg" src="../../img/Mas.png" />
          </div>
          <img class="imageslide" src="../../img/mainScrenshoot.png" />
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
