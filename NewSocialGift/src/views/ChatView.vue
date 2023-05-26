<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
import MiComponente from './../components/separarTrama.vue'

export default {
  components: {
    NavBar,
    language,
    MiComponente
  },
  data() {
    return {
      users: []
    }
  },
  methods: {
    async searchFriend() {
      this.users = []
      document.getElementById('search-results-id').style.display = 'block'
      const criteria = document.getElementById('valor').value
      console.log('valor ' + criteria)
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
          console.log(this.users)
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
    },
    selectFriend(name, image) {
      console.log(name, image)

      document.getElementById('noChats').style.display = 'none'
      document.getElementById('listheader').style.display = 'block'
      document.getElementById('chat-input-id').style.display = 'block'
      document.getElementById('usernameJS').innerHTML = name
      document.getElementById('imageJS').src = image
    }
  },
  mounted() {}
}
</script>

<template>
  <div>
    <language />

    <section id="GeneralSection">
      <NavBar />
      <div id="chat-profiles">
        <div>
          <h1>Search friend</h1>
          <div class="search-container">
            <input
              type="text"
              placeholder="User name..."
              id="valor"
              @keydown.enter="searchFriend"
            />
            <a id="search-button" @click="searchFriend"> Search </a>
          </div>
          <div id="search-results-id" class="search-results">
            <ul v-for="user in users" :key="user.id">
              <li>
                <a @click="selectFriend(user.name, user.image)"
                  ><img :src="user.image" />{{ user.name }}</a
                >
              </li>
            </ul>
          </div>
        </div>
        <div id="list-profiles">
          <ul>
            <li>
              <a><img />NickName</a>
            </li>
            <li>
              <a><img />NickName</a>
            </li>
            <li>
              <a><img />NickName</a>
            </li>
            <li>
              <a><img />NickName</a>
            </li>
          </ul>
        </div>
        <div></div>
      </div>
      <div class="chat-section">
        <h1 id="noChats">Selecciona un chat!</h1>
        <div id="listheader" class="listheader">
          <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" id="imageJS" />
          <h3 id="usernameJS">NickName</h3>
          <a href="#"><i id="moreimg" class="fa-solid fa-info" style="color: #000000"></i></a>
        </div>
        <div class="chat-div">
          <h4 id="messageUser">Lorem Ipsum hoal que tal me allamo apcao</h4>
        </div>
        <div class="chat-input" id="chat-input-id">
          <textarea type="text" id="message" placeholder="Write a message..." />
          <a href="#"><i class="fa-solid fa-paper-plane"></i></a>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
@import '../assets/ChatStyle.css';
</style>
<style>
@media screen and (max-width: 600px) {
  #GeneralSection {
    height: 100% !important;
  }
  #chat-profiles {
    border: 0cm !important;
    margin-top: 40px !important;
    margin-left: -110px;
    width: 105% !important;
  }
  #chat-section {
    visibility: hidden;
  }
}
</style>
