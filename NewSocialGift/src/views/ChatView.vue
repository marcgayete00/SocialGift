<script>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
import MiComponente from './../components/separarTrama.vue'
import io from 'socket.io-client'
import VueSocketIO from 'vue-socket.io'

export default {
  components: {
    NavBar,
    language,
    MiComponente
  },
  data() {
    return {
      users: [],
      showNoResultsMessage: false,
      userMessaged: [],
      messages: [],
      GlobalId: 0,
    }
  },
  methods: {
    async searchFriend() {
      this.users = []
      const criteria = document.getElementById('criteria').value;
      //console.log('criteria ' + criteria)
      document.getElementById('closeResults').style.display = 'block'
      document.getElementById('search-results-id').style.display = 'block'
      document.getElementById('scrolleable-list-id').style.display = 'block'
      
      
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
          for (let i = 0; i < data.length; i++) {
            this.users.push(data[i])
          }

          if (this.users.length === 0) {
            this.showNoResultsMessage = true; // Mostrar el mensaje si no se encuentran resultados
          } else {
            this.showNoResultsMessage = false; // Ocultar el mensaje si se encuentran resultados
          }
          //console.log(this.users)
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })
    },
    selectFriend(name, image, id) {
      this.messages = []
      console.log(name, image)
      localStorage.setItem('CurrentUserToTalkId', id);
      document.getElementById('noChats').style.display = 'none'
      document.getElementById('listheader').style.display = 'block'
      document.getElementById('chat-input-id').style.display = 'block'
      
      document.getElementById('usernameJS').innerHTML = name
      document.getElementById('imageJS').src = image

      const token = localStorage.getItem('accessToken')
      
      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/messages/`+id, {
        method: 'GET',
        headers: {
          contentType: 'application/json',
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
          for (let i = 0; i < data.length; i++) {
            this.messages.push(data[i])
          }
          //console.log(this.users)
        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })

    },

    async sendMessage() {
      var message = document.getElementById('message').value;

      const token = localStorage.getItem('accessToken')
      const id = MiComponente.methods.obtenerIdDesdeToken(token)
      
      const bodymessage = {
        content: message,
        user_id_send: id,
        user_id_recived: parseInt(localStorage.getItem('CurrentUserToTalkId'))
      }

      //enviar mensajes por sockets
      console.log(this.socket.id)
      this.socket.emit('send', message);

      fetch(`https://balandrau.salle.url.edu/i3/socialgift/api/v1/messages`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${token}`
        },
        body: JSON.stringify(bodymessage)
      })
        .then((response) => {
          if (response.ok) {
            //console.log("Mensaje enviado correctamente");
            return response.json();
          } else {
            throw new Error('Error en la petición');
          }
        })
        .then((data) => {
          //console.log(data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    closeResults(){
      this.users = []
      document.getElementById('closeResults').style.display = 'none'
      document.getElementById('scrolleable-list-id').style.display = 'none'
    }
  },
  mounted() {

    this.socket = io("https://balandrau.salle.url.edu", {path: "/i3/socialgift/socket.io"});

    if (this.socket) {
      console.error("mySocket is not null and not undefined");
      this.socket.on('connect', () => {
        console.log("Connected to server");
        console.log(this.socket.id);
      });

      // Agregar el listener para el evento 'message'
      this.socket.on('send', (data) => {
        console.log("Mensaje recibido:", data);
        // actualizar el estado de tu componente con el mensaje recibido y mostrarlo en la pantalla
        this.messages.push(data)
      });
    } else {
      console.error("mySocket is null or undefined");
    }

    const token = localStorage.getItem('accessToken')
    const id = MiComponente.methods.obtenerIdDesdeToken(token)
    this.GlobalId = id;
    console.log(this.GlobalId)
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
              placeholder="User name..." id="criteria"
              @keydown.enter="searchFriend"
            />
            <a id="search-button" @click="searchFriend"> Search </a>
          </div>
          <div id="search-results-id" class="search-results">
              <i class="fa-solid fa-xmark" id="closeResults" @click="closeResults"></i>
              <div class="scrollable-list" id="scrolleable-list-id">
                <ul v-for="user in users" :key="user.id">
                  <li>
                    <a @click="selectFriend(user.name, user.image, user.id)">
                      <img :src="user.image" />
                      {{ user.name }}
                    </a>
                  </li>
                </ul>
                <p v-show="showNoResultsMessage && users.length === 0" id="no-results-message">No results</p>
              </div>
              
            </div>
        </div>
        <div id="list-profiles" >
          <ul v-for="user in userMessaged" :key="userMessaged.id"  >
            <li>
              <a @click="selectFriend(user.name, user.image, user.id)"><img :src="user.image" />{{user.name}}</a>
            </li>
          </ul>
        </div>
        <div></div>
      </div>
      <div class="chat-section">
        <h1 id="noChats">Selecciona un chat!</h1>
        <div id="listheader" class="listheader">
          <img class="profileimglist" id="imageJS" />
          <h3 id="usernameJS"></h3>
        </div>
        <div class="chat-div" >
          <ul v-for="message in messages" :key="message.id">
            <li>
               <a v-if="message.user_id_send == this.GlobalId" id="YourMessage">{{message.content}}</a>
               <a v-else id="TheirMessage">{{message.content}}</a>
            </li>
          </ul>
        </div>
        <div class="chat-input" id="chat-input-id">
          <input type="text" id="message" placeholder="Write a message..." @keydown.enter="sendMessage" maxlength="45">
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
