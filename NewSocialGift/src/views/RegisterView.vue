<script>
import language from './../components/language.vue'

export default {
  components: {
    language
  },
  data() {
  },
  methods: {
    addUser() {
      const user = {
        name: document.getElementById('username').value,
        last_name: document.getElementById('surname').value,
        email: document.getElementById('email').value,
        password: document.getElementById('password').value,
        image: document.getElementById('file-upload').value,
      }

      fetch('https://balandrau.salle.url.edu/i3/socialgift/api/v1/users', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(user)
      })
        .then((response) => {
          if (response.status === 201) {
            alert('User added')
            window.location.replace('/')
          } else {
            console.log('hey')
            switch (response.status) {
              case 404:
                alert('An error has occurred')
                break

              case 401:
                alert('Wrong email or password')
                break

              case 406:
                alert('Missing parameters')
                break

              case 409:
                alert('Missing parameters')
                break

              default:
                alert('An error has occurred')
                break
            }
          }
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<template>
  <div>
    <language :show-hamburguer-menu="false" />
    <section id="GeneralSectionRegister">
      <section id="RegisterSection">
        <div>
          <img src="img/logo.png" id="LogoStyle" />
          <form onsubmit="return false">
            <input type="text" class="inputRegister" id="username" placeholder="Usuario..." /><br />
            <input type="text" class="inputRegister" id="surname" placeholder="Surname..." /><br />
            <input type="text" class="inputRegister" id="email" placeholder="E-mail..." /><br />
            <input
              type="password"
              class="inputRegister"
              id="password"
              name="password"
              placeholder="Contraseña..."
            /><br />

            <div class="file-upload-wrapper">
              <input id="file-upload" class="inputRegister" name="file" accept="image/*" placeholder="Profile photo URL (http://...)" />
            </div>

            <button id="registerButton" @click="addUser"><a> Siguiente </a></button>
          </form>
        </div>
      </section>
    </section>

    <section id="GeneralSectionRegister2">
      <section id="RegisterSection2">
        <span id="textRegister2">¿You have already an account?<a href="/"> Log-in</a></span>
      </section>
    </section>
  </div>

  <footer id="registerFooter">
    <div>
      <nav>
        <ol class="footerList2">
          <li><a href="#">Help</a></li>
          <li><a href="#">Privacy</a></li>
          <li><a href="#">Terms</a></li>
        </ol>
      </nav>
    </div>
  </footer>
</template>

<style>
@media screen and (max-width: 600px) {
  #LogoStyle {
    width: 200px !important;
    height: 60px !important;
    margin-left: 50px !important;
    margin-top: 20px;
  }

  #GeneralSectionRegister {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #RegisterSection {
    width: 300px;
    margin-top: 20px;
  }

  .inputRegister {
    width: 280px !important;
    margin-right: 20px;
  }

  #GeneralSectionRegister2 {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 350px;
    margin-bottom: 50px !important;
  }

  #RegisterSection2 {
    margin-top: 400px;
  }
  #registerFooter {
    display: none;
  }

  .upload-btn {
    width: 250px !important;
  }


  #registerButton {
    width: 250px !important;
    height: 50px !important;
    margin-left: 25px !important;
    margin-bottom: 30px;
  }

  #RegisterSection2 {
    width: 210% !important;
    height: 30% !important;
    margin-top: 250px !important;
    padding-top: 7px !important;
  }

  #textRegister2 {
    font-size: small !important;
    margin-left: 20px !important;
    padding-bottom: 10px !important;
  }

  #textRegister2 a {
    font-size: large !important;
  }
}
</style>

<style scoped>
@import '../assets/HomeStyle.css';
</style>
