<script>
export default {
  methods: {
    logout() {
      localStorage.removeItem('accessToken')
      this.$router.push('/')
    },
    async searchFriend() {
      this.users = []
      document.getElementById('search-results').style.display = 'block'
      const criteria = document.getElementById('search-friend').value
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
          console.log(data)
          for (var i = 0; i < data.length; i++) {
            this.users.push(data[i])
          }
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
    }
  }
}
</script>

<template>
  <div class="navigation">
    <ul>
      <li>
        <a href="main"> <img src="../../img/logo.png" id="logoNavBar" alt="" /></a>
      </li>
      <li>
        <a href="main"><i class="fa-solid fa-house"></i> Home</a>
      </li>
      <li>
        <a href="#"><i class="fa-solid fa-magnifying-glass"></i> Search</a>
        <ul id="SearchSlide">
          <li>
            <div class="search-container">
              <input
                type="text"
                placeholder="User name..."
                id="search-friend"
                @keydown.enter="searchFriend"
              />
              <a id="search-button" @click="searchFriend"> Search </a>
            </div>
            <div id="search-results" class="search-results">
              <ul v-for="user in users" :key="user.id">
                <li>
                  <a @click="selectFriend(user.name, user.image)"
                    ><img :src="user.image" />{{ user.name }}</a
                  >
                </li>
              </ul>
            </div>
          </li>
        </ul>
      </li>
      <li>
        <a href="chat"><i class="fa-solid fa-envelope"></i> Messages</a>
      </li>
      <li>
        <a href="#"><i class="fa-sharp fa-solid fa-bell"></i> Notifications</a>
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
        <a href="createList"><i class="fa-solid fa-pen-to-square"></i> Create</a>
      </li>
      <li id="MoreLi">
        <a href="#"><i class="fa-solid fa-bars"></i> More</a>
        <ul id="moreSlide">
          <li><a href="editarperfil">Editar Perfil</a></li>
          <li><a href="#" @click="logout">Desconectar</a></li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<style scoped>
@import '../assets/NavBar.css';
</style>
