<script setup>
import NavBar from './../components/NavBar.vue'
import language from './../components/language.vue'
</script>

<template>
    <div>
      <language />

      <section id="GeneralSection">
        <NavBar />
        <div id="chat-profiles">
            <div>
                <img class="iconocrear" src="../../img/Crear.png">
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
