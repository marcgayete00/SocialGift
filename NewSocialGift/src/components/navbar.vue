<script>
import MiComponente from './../components/separarTrama.vue'


export default {
  data() {
    return {
      mainID: null,
      hasNotifications: false, // Estado de las notificaciones
      users: []
    }
  },
  methods: {
    async showS(){
      document.getElementById('close-buttonN').style.display = 'none';
      document.getElementById('close-buttonS').style.display = 'block';
      document.getElementById('SearchSlide').style.display = 'block';
      if(document.getElementById('NotificationsSlide').style.display == 'block'){
        document.getElementById('NotificationsSlide').style.display = 'none';
      }
    },

    async showN(){
      document.getElementById('close-buttonS').style.display = 'none';
      document.getElementById('close-buttonN').style.display = 'block';
      document.getElementById('NotificationsSlide').style.display = 'block';
      if(document.getElementById('SearchSlide').style.display == 'block'){
        document.getElementById('SearchSlide').style.display = 'none';
      }
      await this.getFriendRequests();
    },

    async showM(){
      if(document.getElementById('moreSlide').style.display == 'block'){
        document.getElementById('moreSlide').style.display = 'none';
      }else{
        document.getElementById('moreSlide').style.display = 'block';
      }
    },

    async closeS(){
      document.getElementById('close-buttonS').style.display = 'none';
      document.getElementById('close-buttonN').style.display = 'none';
      document.getElementById('SearchSlide').style.display = 'none';
    },

    async closeN(){
      document.getElementById('close-buttonS').style.display = 'none';
      document.getElementById('close-buttonN').style.display = 'none';
      document.getElementById('NotificationsSlide').style.display = 'none';
      
    },

    async logout() {
      localStorage.removeItem('accessToken')
      this.$router.push('/')
    },

    async RedirectUser(userID) {
      window.location.href = '/profile/' + userID
    },

    async getFriendRequests() {
      this.users = [];
      const token = localStorage.getItem('accessToken');

      fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/friends/requests', {
        method: 'GET',
        headers: {
          Authorization: `Bearer ${token}`,
          Accept: 'application/json'
        }
      })
        .then(response => {
          if (response.status === 200) {
            return response.json();
          } else {
            throw new Error('Error al obtener las solicitudes de amistad');
          }
        })
        .then(data => {
          // Actualizar el arreglo users con las solicitudes de amistad
          for (let i = 0; i < data.length; i++) {
            this.users.push(data[i]);
          }
        })
        .catch(error => {
          console.error(error);
          // Manejo de errores en caso de falla de la solicitud
        });
    },
    
    async addFriend(userId) {
      const token = localStorage.getItem('accessToken');

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/friends/${userId}`, {
        method: 'POST',
        headers: {
          Authorization: `Bearer ${token}`,
          Accept: 'application/json'
        }
      })
        .then(response => {
          if (response.status === 201) {
            // Aquí puedes realizar acciones adicionales después de enviar la solicitud
            console.log('Solicitud de amistad enviada con éxito');
          } else {
            throw new Error('Error al enviar la solicitud de amistad');
          }
        })
        .catch(error => {
          console.error(error);
          // Manejo de errores en caso de falla de la solicitud
        });
    }, 

    async acceptFriend(userId) {
      const token = localStorage.getItem('accessToken');

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/friends/${userId}`, {
        method: 'PUT',
        headers: {
          Authorization: `Bearer ${token}`,
          Accept: 'application/json'
        }
      })
        .then(response => {
          if (response.status === 200) {
            // Aquí puedes realizar acciones adicionales después de aceptar la solicitud
            console.log('Solicitud de amistad aceptada');
          } else {
            throw new Error('Error al aceptar la solicitud de amistad');
          }
        })
        .catch(error => {
          console.error(error);
          // Manejo de errores en caso de falla de la solicitud
        });
        window.location.reload();
    },

    async denyFriend(userId) {
      const token = localStorage.getItem('accessToken');

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/friends/${userId}`, {
        method: 'DELETE',
        headers: {
          Authorization: `Bearer ${token}`,
          Accept: 'application/json'
        }
      })
        .then(response => {
          if (response.status === 200) {
            // Aquí puedes realizar acciones adicionales después de denegar la solicitud
            console.log('Solicitud de amistad denegada');
          } else {
            throw new Error('Error al denegar la solicitud de amistad');
          }
        })
        .catch(error => {
          console.error(error);
          // Manejo de errores en caso de falla de la solicitud
        });
      window.location.reload();
    },

    async searchFriend() {
      this.users = []
      document.getElementById('search-results-id').style.display = 'block'
      const criteria = document.getElementById('valor').value
      const token = localStorage.getItem('accessToken')

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/users/search?s=${criteria}`, {
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
          for (var i = 0; i < data.length; i++) {
            this.users.push(data[i])
          }
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
        console.log(this.users)
    },
    closeNavBarFunction(){
      document.getElementsByClassName('navigation')[0].style.display = 'none';
    }
  },
  mounted() {
    this.users = [];
    const token = localStorage.getItem('accessToken');
    const id = MiComponente.methods.obtenerIdDesdeToken(token)
    this.mainID = id;
    fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/friends/requests', {
      method: 'GET',
      headers: {
        Authorization: `Bearer ${token}`,
        Accept: 'application/json'
      }
    })
      .then(response => {
        if (response.status === 200) {
          return response.json();
        } else {
          throw new Error('Error al obtener las solicitudes de amistad');
        }
      })
      .then(data => {
        // Actualizar el arreglo users con las solicitudes de amistad
        for (let i = 0; i < data.length; i++) {
          this.users.push(data[i]);
        }

        if(data.length > 0){
          this.hasNotifications = true;
        }
      })
      .catch(error => {
        console.error(error);
        // Manejo de errores en caso de falla de la solicitud
      });
      
  }
}
</script>

<template>
  <div class="navigation">
    <ul>
      <li>
        <a href="/main"> <img src="../../img/logo.png" id="logoNavBar" alt="" /></a>
      </li>
      <li>
        <a href="/main"><i class="fa-solid fa-house"></i> Home</a>
      </li>
      <li id="navprofile">
        <a @click="RedirectUser(mainID)"><i class="fa-solid fa-user"></i> Profile</a>
      </li>
      <li>
        <a @click="showS()"><i class="fa-solid fa-magnifying-glass" ></i> Search</a>
        <button @click="closeS()" id="close-buttonS"><i class="fa-solid fa-xmark"></i></button>
        <ul id="SearchSlide">
          <li>
            <div class="search-container">
            <input
              type="text"
              placeholder="Username..."
              id="valor"
              @keydown.enter="searchFriend"
            />
            <a id="search-button" @click="searchFriend"> Search </a>
          </div>
          <div id="search-results-id" class="search-results">
            <ul v-for="user in users" :key="user.id">
              <li>
                <a @click="RedirectUser(user.id)"><img :src="user.image" />{{ user.name }}</a>
              </li>
              <button v-if="user.id != this.mainID" id="add-button" @click="addFriend(user.id)">Enviar Solicitud</button>
              <button v-else id="add-button" disabled>Enviar Solicitud</button>

            </ul>
          </div>
          </li>
        </ul>
      </li>
      <li>
        <a href="/chat"><i class="fa-solid fa-envelope"></i> Messages</a>
      </li>
      <li>
        <a @click="showN()">
          <i v-if="this.hasNotifications === true" class="fa-solid fa-bell fa-shake"></i> 
          <i v-else class="fa-sharp fa-solid fa-bell"></i>
          Notifications</a>
        <button @click="closeN()" id="close-buttonN"><i class="fa-solid fa-xmark"></i></button>
        <ul id="NotificationsSlide">
          <li style="font-size: larger">Más recientes</li>
          <div id="notifications-results-id">
            <ul v-for="user in users" :key="user.id">
              <li>
                <a><img :src="user.image" />{{ user.name }}</a>
                <button id="accept-button" @click="acceptFriend(user.id)">Aceptar</button>
                <button id="deny-button" @click="denyFriend(user.id)">Denegar</button>
              </li>
              
            </ul>
          </div>
          </ul>
      </li>
      <li>
        <a href="/createList"><i class="fa-solid fa-pen-to-square"></i> Create</a>
      </li>
      <li id="navlogout">
        <a @click="logout"><i class="fa-solid fa-right-from-bracket"></i> Logout</a>
      </li>
      <li id="MoreLi">
        <a @click="showM()"><i class="fa-solid fa-bars"></i> More</a>
        <ul id="moreSlide">
          <li><a href="/editarperfil">Editar Perfil</a></li>
          <li><a href="#" @click="logout">Desconectar</a></li>
        </ul>
      </li>
      <li>
        <a @click="closeNavBarFunction()"><i id="closeNavBar" class="fa-solid fa-bars"></i></a>
      </li>
    </ul>
  </div>
</template>

<style scoped>
@import '../assets/NavBar.css';

@media screen and (max-width: 600px) {
  .navigation{
   width: 100% !important;
  }

  #navlogout{
    display: block !important;
  }

  #navprofile{
    display: block !important;
  }

  .navigation li{
    margin-left: 100px !important; 
  }

  #closeNavBar{
    display: block;
    font-size: 40px;
    margin-top: -1025px;
    margin-left: 200px;
  }
}

</style>