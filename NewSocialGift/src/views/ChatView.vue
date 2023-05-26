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
      users: [],
      userMessaged: []
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
    selectFriend(name, image, id) {
      console.log(name, image)
      localStorage.setItem('CurrentUserToTalkId', id);
      document.getElementById('noChats').style.display = 'none'
      document.getElementById('listheader').style.display = 'block'
      document.getElementById('chat-input-id').style.display = 'block'
      document.getElementById('usernameJS').innerHTML = name
      document.getElementById('imageJS').src = image
      document.getElementById('messageUser').style.display = 'none'
    },

    async sendMessage() {
      var message = document.getElementById('message').value;
      const token = localStorage.getItem('accessToken')
      const id = MiComponente.methods.obtenerIdDesdeToken(token)
      
      const bodymessage = {
        content: message,
        user_id_send: id,
        user_id_recived: localStorage.getItem('CurrentUserToTalkId')
      }

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/messages`, {
        method: 'POST',
        headers: {
          Authorization: `Bearer ${token}`,
          
        },
        body: JSON.stringify(bodymessage)
      })
        .then((response) => {
          if (response.status === 200) {
            console.log("Mensaje enviado correctamente");
            return response.json()
          } else {
            console.log(response)
          }
        })
        .then((data) => {
          console.log(data);
        })
        .catch((error) => {
          console.log(error);
        });
    }
  },
  mounted() {
    fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/messages/users', {
      method: 'GET',
      headers: {
        Authorization: `Bearer ${localStorage.getItem('accessToken')}`,
        'Content-Type': 'application/json'
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
          this.userMessaged.push(data[i])
        }
        console.log(this.userMessaged)
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
                <a @click="selectFriend(user.name, user.image, user.id)"><img :src="user.image" />{{ user.name }}</a
                >
              </li>
            </ul>
          </div>
        </div>
        <div id="list-profiles" >
          <ul v-for="user in userMessaged" :key="userMessaged.id">
            <li>
              <a><img :src="user.image" />{{user.name}}</a>
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
          <input type="text" id="message" placeholder="Write a message..." @keydown.enter="sendMessage">
          <a @keydown.enter="sendMessage"><i class="fa-solid fa-paper-plane"></i></a>
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
