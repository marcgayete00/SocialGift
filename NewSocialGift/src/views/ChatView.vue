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
      
    }
  },
  methods: {
    async searchFriend(){
      const criteria = document.getElementById('search-friend').value;
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
          for(var i = 0; i < data.length; i++){
            if (data[i].name === criteria){
              console.log(data)
              document.getElementById("usernameJS").innerHTML = data[i].name;
              document.getElementById("imageJS").src = data[i].image;
            }
          }
          


        })
        .catch((error) => {
          //Respuesta en caso de error de servidor
        })

    }
    
    
  },
  mounted() {
    
  },

}


</script>

<template>
    <div>
      <language />

      <section id="GeneralSection">
        <NavBar />
        <div id="chat-profiles">
            <div>
                <h1> Search friend </h1>
                <div class="search-container">
                    <input type="text" placeholder="User name..." id="search-friend" />
                    <a id="search-button" @click="searchFriend"> Search </a>
                </div>
            </div>
            <div id="list-profiles">
                <ul>
                    <li><a><img>NickName</a></li>
                    <li><a><img>NickName</a></li>
                    <li><a><img>NickName</a></li>
                    <li><a><img>NickName</a></li>
                </ul>
            </div>
            <div>

            </div>
        </div>
        <div class="chat-section">
            <div class="listheader">
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png" id="imageJS">
                <h3 id="usernameJS">NickName</h3>
                <a href="#"><i id="moreimg" class="fa-solid fa-info" style="color: #000000;"></i></a>
            </div>
            <div id="chatdiv">
                
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
        #chat-profiles{
            border: 0cm !important;
          margin-top: 40px !important;
          margin-left: -110px;
          width: 105% !important;
        
        }
        #chat-section{
            visibility: hidden;
        }
    }
</style>
