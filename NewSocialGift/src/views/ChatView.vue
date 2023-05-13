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
                    <a id="search-button"> Search </a>
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
                <img class="profileimglist" src="../../img/DefaultProfilePhoto.png">
                <h3>NickName</h3>
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
