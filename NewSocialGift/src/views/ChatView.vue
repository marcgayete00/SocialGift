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
      newMessage: [],
      newMessageSent: [],
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
      this.newMessage = []
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

      const accessToken = {
        "accessToken": token
      };
      console.log(accessToken)
      //hacer un envio de mensajes por socket.io
      this.socket.emit("query_user", JSON.stringify(bodymessage));
      this.socket.emit("send_msg", JSON.stringify(bodymessage));

      
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
    },
    toggleTaskBar(){
      const navigation = document.querySelector('.navigation');
      if (navigation) {
        navigation.style.display = 'block';
      }
    },
    goProfileUser(){
      window.location.href = '/profile/' + localStorage.getItem('CurrentUserToTalkId')
    },
  },
  mounted() {

    const tokenEmit = localStorage.getItem('accessToken')
    this.socket = io("https://balandrau.salle.url.edu", {path: "/i3/socialgift/socket.io"});

    if (this.socket) {
      console.error("mySocket is not null and not undefined");
      this.socket.on('connect', () => {
        console.log("Connected to server");
        console.log(this.socket.id);
        this.socket.emit("login", `${tokenEmit}`);
        //this.socket.emit("login", JSON.stringify({"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTIxLCJlbWFpbCI6ImFkbWluc0BnbWFpbC5jb20iLCJpYXQiOjE2ODU2OTc3Mzl9.34S-_iU06GeaObnPqCJkugi2czCeMXquj05XgIqnwXY"}));
      });
    
      this.socket.on("save_msg", (saveMsg) => {
        //Enviar mensaje 
        console.log("Mensaje recibido: " + saveMsg); 
        console.log("Enviando mensaje")
      });

      this.socket.on("send_msg", (sendMsg) => {
        //Obtener el cotenido del mensaje 
        console.log("sendMsg => " + sendMsg)
        this.newMessageSent.push(document.getElementById('message').value = '');
        console.log(this.newMessageSent)   
      });

      this.socket.on("query_user", (queryUser) => {
        //Obtener el cotenido del mensaje 
        console.log("queryUser => " + queryUser )  
      });

      this.socket.on("historic_msg", (historicMsg) => {
        //Obtener el cotenido del mensaje 
        console.log("historicMsg => " + historicMsg )  
      });

      this.socket.on("new_msg", (newMsg) => {
        console.log("newMsg => " + newMsg)
        const message = newMsg.split('"');
        this.newMessage.push(message[3])
        //mostrar el mensaje en el chat
      
      });

      this.socket.on("connect_error", (error) => {
        console.log("TransportError:", error);
      });

      this.socket.on("login", (login) => {
        console.log("login => " + login )
      });

      this.socket.on("disconnect", (reason) => {
        console.log("disconnect:");
        setTimeout(() => {
          socket.connect();
        }, 1000);
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
    <a @click="toggleTaskBar()" class="togleNavBar" ><i class="fa-solid fa-bars"></i></a>
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
          <h3 @click="goProfileUser()" id="usernameJS"></h3>
        </div>
        <div class="chat-div" >
          <ul v-for="message in messages" :key="message.id">
            <li>
               <a v-if="message.user_id_send == this.GlobalId" id="YourMessage">{{message.content}}</a>
               <a v-else id="TheirMessage">{{message.content}}</a>
            </li>
          </ul>
          <!--Mostrar en el chat mensaje al enviar-->
          
          <!--Mostrar en el chat mensaje al recibir-->
          <ul id="newTheirMessage">
            <li v-for="message in newMessage" :key="message.id">
              <a>{{ message }}</a>
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
    width: 100% !important;
  }
  #chat-profiles {
    border: 0cm !important;
    margin-top: 40px !important;
    margin-left: -110px;
    width: 105% !important;
  }
  
  .listheader{
    width: 100% !important;
  }

  .listheader h3{
    font-size: larger !important;
  }

  #imageJS{
    position: relative !important;
    width: 50px !important;
    height: 50px !important;
    left: 420px !important;
    top: 20px;
  }

  .chat-div{
    width: 100% !important;
  }
  
  #TheirMessage{
    font-size: small !important;
  }

  #YourMessage{
    margin-left: -260px !important;
    font-size: small !important;
  }
  


}
</style>
