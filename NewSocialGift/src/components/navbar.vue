<script>
export default {
  data() {
    return {
      users: []
    }
  },
  methods: {
    async showS(){
      document.getElementById('close-buttonS').style.display = 'block';
      document.getElementById('SearchSlide').style.display = 'block';
      if(document.getElementById('NotificationsSlide').style.display == 'block'){
        document.getElementById('NotificationsSlide').style.display = 'none';
      }
    },

    async showN(){
      document.getElementById('close-buttonN').style.display = 'block';
      document.getElementById('NotificationsSlide').style.display = 'block';
      if(document.getElementById('SearchSlide').style.display == 'block'){
        document.getElementById('SearchSlide').style.display = 'none';
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
                <a><img :src="user.image" />{{ user.name }}</a>
              </li>
            </ul>
          </div>
          </li>
        </ul>
      </li>
      <li>
        <a href="/chat"><i class="fa-solid fa-envelope"></i> Messages</a>
      </li>
      <li>
        <a @click="showN()"><i class="fa-sharp fa-solid fa-bell"></i> Notifications</a>
        <button @click="closeN()" id="close-buttonN"><i class="fa-solid fa-xmark"></i></button>
        <ul id="NotificationsSlide">
          <li style="font-size: larger">Más recientes</li>
          <li id="InsideNotificationSlide">
            <i class="fa-solid fa-user"></i>
            <a>Patricia96</a>
            <p>Te ha empezado a seguir</p>
            <button>Seguir</button>
          </li>
        </ul>
      </li>
      <li>
        <a href="/createList"><i class="fa-solid fa-pen-to-square"></i> Create</a>
      </li>
      <li id="MoreLi">
        <a href="#"><i class="fa-solid fa-bars"></i> More</a>
        <ul id="moreSlide">
          <li><a href="/editarperfil">Editar Perfil</a></li>
          <li><a href="#" @click="logout">Desconectar</a></li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<style scoped>
@import '../assets/NavBar.css';
</style>
