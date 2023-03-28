<template>
  <section id="LanguageSection">
    <nav>
      <ol id="LanguageList">
        <li>
          <img id="switchImg" src="../components/icons/ds.png" />
        </li>
        <li id="switchLi">
          <label class="switch">
            <input type="checkbox" />
            <span class="slider"></span>
          </label>
        </li>
        <li>
          <select name="select" id="LanguageSelect">
            <option value="value1" selected>Spanish</option>
            <option value="value2">English</option>
          </select>
        </li>
        <div>
          <navBar :showNavbar="showNavbar" />
          <li id="hamburguerMenu"><a href="#" @click="toggleNavbar"><i class="fa-solid fa-bars"></i></a></li>
        </div>
      </ol>
    </nav>
  </section>
</template>



<style scoped>
@import '../assets/language.css';
</style>

<script>
  import navBar from './navBar.vue'

  export default {
    data() {
      return {
        showNavbar: false
      }
    },
    methods: {
      toggleNavbar() {
        this.showNavbar = !this.showNavbar
      }
    },
    components: {
      navBar
    }
  }
</script>
<style>



  @media screen and (max-width: 600px) {
    #hamburguerMenu a{
      text-decoration: none;
      color: black;
    }

    #hamburguerMenu i{
      display: block !important;
      font-size: 40px!important;
      margin-left: 100px; ;
  }

    .NavBar {
    display: none;
  }

  .NavBar--show {
    display: block;
  }
    
  }

</style>
